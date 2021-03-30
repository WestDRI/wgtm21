+++
title = "Plotting with cartopy"
slug = "python-15-cartopy"
weight = 15
+++

## Plotting with cartopy

Cartopy lets you process your geospatial data in order to produce maps, e.g. using various map projections. All plotting
is still being done by Matplotlib.

```py
import cartopy.crs as ccrs
import matplotlib.pyplot as plt
import cartopy.feature as cfeature
fig = plt.figure(figsize=(12,12))
ax = fig.add_subplot(111, projection=ccrs.PlateCarree())
ax.coastlines()
ax.coastlines(resolution='50m', color='gray', linewidth=2)   # valid scales are "110m", "50m", "10m"
ax.add_feature(cfeature.OCEAN)
ax.add_feature(cfeature.LAND)
ax.add_feature(cfeature.BORDERS, linestyle=':')
```

Try the following projections (and bring online help on these):

- PlateCarree(0) is the equi-rectangular/Cartesian projection (meridians are vertical straight lines)
- Orthographic(-100,55)
- Mollweide(0)
- Robinson(0)
- InterruptedGoodeHomolosine(0)

[More information](https://scitools.org.uk/cartopy/docs/latest/crs/projections.html#cartopy-projections) on cartopy projections.

Let's only plot North America:

```py
fig = plt.figure(figsize=(12,12))
ax = fig.add_subplot(111, projection=ccrs.Mollweide(-100))
ax.coastlines()
ax.add_feature(cfeature.OCEAN)
ax.add_feature(cfeature.LAND)
ax.add_feature(cfeature.BORDERS, linestyle=':')
ax.set_extent([-160, -51, 5, 85])
```

You can zoom in much further, and the high-resolution data will be downloaded from online sources. E.g. let's focus on
Vancouver Island:

```py
fig = plt.figure(figsize=(12,12))
ax = fig.add_subplot(111, projection=ccrs.PlateCarree())
ax.coastlines()
ax.add_feature(cfeature.OCEAN)
ax.add_feature(cfeature.LAND)
ax.add_feature(cfeature.BORDERS, linestyle=':')
ax.set_extent([-129, -122, 46, 53])
```

Let's overlay the Natural Earth shaded relief on top of our map and display the night shade:

```py
fig = plt.figure(figsize=(14,12))
ax = fig.add_subplot(111, projection=ccrs.Mollweide())
ax.stock_img()   # add the Natural Earth shaded relief image
ax.add_feature(cfeature.BORDERS, linestyle=':')

import datetime
import pytz
date = datetime.datetime.now()   # local time now
utc = datetime.datetime.utcnow()   # UTC time now
date, utc

from cartopy.feature.nightshade import Nightshade
ax.add_feature(Nightshade(utc, alpha=0.2))
```

Let's plot 1D data (a line connecting two points on top of our map):

```py
import cartopy.crs as ccrs
import matplotlib.pyplot as plt

fig = plt.figure(figsize=(12,12))
ax = plt.axes(projection=ccrs.Robinson(-150))
ax.stock_img()

vancouver = (-123.12, 49.28)
perth = (115.86, -31.95)

lon = [vancouver[0], perth[0]]
lat = [vancouver[1], perth[1]]

plt.plot(lon, lat, color='blue', linewidth=2, marker='o')   # does not work!
```

We need to tell matplotlib that our line is a straight line in spherical geometry:

```py
plt.plot(lon, lat, color='blue', linewidth=2, marker='o', transform=ccrs.Geodetic())
```

If you want to add a straight line in planar geometry:

```py
plt.plot(lon, lat, color='gray', linestyle='--', transform=ccrs.PlateCarree())
```

Most matplotlib plotting functions will work with cartopy projections: lines (`plot`), heatmaps and images (`plot` or
`imshow`), scatter plots (`scatter`), vector plots (`quiver`). Let's plot our 2D atmospheric data with Cartopy
projections. Read the data again:

```py
import xarray as xr
data = xr.open_dataset('tasReduced.nc')
temp = data.tas.sel(time="2014-12-16") - 273.15   # extract last timestep, convert to Celsius
temp.shape      # (1, 64, 128)
temp.coords    # the coordinates are 1D, so plotting is easy
```

The data is defined on a 2D Cartesian projection. First, let's plot data in the same projection:

```py
import cartopy.crs as ccrs
import matplotlib.pyplot as plt
fig = plt.figure(figsize=(14,12))
ax = fig.add_subplot(111, projection=ccrs.PlateCarree())
ax.coastlines()
ax.gridlines()
temp.plot(ax=ax, cbar_kwargs={'shrink': 0.4})   # since we are using PlateCarree(), Cartopy assumes
                                                # that the data is also in PlateCarree() coordinates, which is true
```

Now let's switch the projection. Then we have to tell Cartopy our data's coordinate system explicitly with `transform`:

```py
fig = plt.figure(figsize=(14,12))
ax = fig.add_subplot(111, projection=ccrs.InterruptedGoodeHomolosine())   # use this projection
ax.coastlines()
ax.gridlines()
temp.plot(ax=ax, transform=ccrs.PlateCarree(), cbar_kwargs={'shrink': 0.4})
            # `transform` tells Cartopy the coordinate system of our data
```

Let's switch the projection and zoom in on Vancouver Island:

```py
ax = fig.add_subplot(111, projection=ccrs.Mollweide(-125))
ax.coastlines()
ax.gridlines()
temp.plot(ax=ax, transform=ccrs.PlateCarree(), cbar_kwargs={'shrink': 0.4})
ax.set_extent([-129, -122, 46, 53])
```

We can see that our data is really low resolution.
