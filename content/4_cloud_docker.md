+++
title = "Docker"
slug = "cloud_docker"
+++

{{<cor>}}Tuesday, June 29{{</cor>}}\
{{<cgr>}}9 am–12 pm Pacific Time{{</cgr>}}

**Instructor**: Jacob Boschee (UBC)

**Target audience**: general

**Level**: beginner

**Prerequisites**: [Introduction to Compute Canada cloud](../cloud) course

We will be running Docker inside virtual machines (VMs) in Compute Canada cloud, so you must be familiar
with setting up a blank Ubuntu server in a cloud VM before attending this course.

**Software**: All attendees will need a remote secure shell (SSH) client installed on their computer in
order to participate in the course exercises. On Windows we recommend
[the free Home Edition of MobaXterm](https://mobaxterm.mobatek.net/download.html). On Mac and Linux
computers SSH is usually pre-installed (try typing `ssh` in a terminal to make sure it is there).

Materials to download:
* [PDF slides](../../slides/docker.pdf)
* [raw text document](/other/dockerCommands.txt) with all commands
* Gnuplot [example script](/other/pm3d_lighting.2.gnu)

{{<cor>}}Zoom{{</cor>}} {{<s>}} {{<cgr>}}9:00am-12:00pm Pacific{{</cgr>}} \
{{<nolinktitle>}}Live session in 30-40 min presentation blocks{{</nolinktitle>}}

<!-- last year https://wgschool.netlify.app/docker -->

## Exercises
#### Exercise 1: Hello Docker!

{{< yt ikuqAPT3F44 63 >}}

In this exercise we will install docker on our VM and run the test Hello World docker. Before continuing
with this exercise please be sure you have an Ubuntu (or CentOS) VM set up that you are able to log
into. For details on setting up a VM with your guest account, check [these PDF slides](../ccCloud.pdf)
from yesterday's CC Cloud course or the videos [therein](../cloud).

Once you are logged into your VM, and you are using Ubuntu, please follow along with the video and
execute the following commands (one command at a time!):

```
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
sudo docker run hello-world
```

If you are working with a CentOS VM (following yesterday's cloud course), then the commands for this
exercise are:

```
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install wget docker-ce docker-ce-cli containerd.io 
sudo systemctl start docker
sudo docker run hello-world
```

#### Exercise 2: Setting up a CentOS Docker Container

{{< yt LZ39p1sMsmg 63 >}}

In this exercise we will use Docker to download and run a copy of CentOS on our Ubuntu VM. To follow
along with the exercise video, please use the following list of commands (one command at a time!):

```
sudo docker images
sudo docker search centos
sudo docker pull centos
sudo docker run -it --name First_Centos centos
cat /etc/redhat-release
```

#### Exercise 3: Working within a Docker Container and Host Connections

{{< yt GWyRoSq0j_U 63 >}}

In this exercise we will be using Docker to create a container for running gnuplot. To pass the output
files from gnuplot back to our host system we will set up a mount volume attached to a folder in the
host. To follow along with the exercise video please use the following list of commands (one command at a
time!):

```
mkdir ~/input
sudo docker run -it --name gnuPlotExample -v ~/input:/workdir centos
yum install gnuplot
cd /workdir
wget https://wgschool.netlify.app/docker/pm3d_lighting.2.gnu
gnuplot /workdir/pm3d_lighting.2.gnu
exit
```

Once complete with the commands, use MobaXTerm’s file browser to locate `pm3d_lighting.2.png` within the
inputs folder to view the output of gnuplot.

#### Exercise 4: Building Docker Images for Portability

{{< yt 2Ez0w42qGwE 63 >}}

In this exercise we will use a Dockerfile to create a CentOS image with gnuplot already installed and
ready to execute on a mounted volume. We will then repeat the results of Exercise 3 with this new image
without using an interactive shell. Finally we will save and reimport a copy of the image we created to
demonstrate the ability to port Docker images to other systems. To follow along with the exercise video,
please use the following command:

```
nano Dockerfile
```

and then type the following into the file `Dockerfile`:

```
#CentOS GNUPlot
FROM centos
VOLUME /workdir
WORKDIR /workdir
RUN yum install gnuplot -y
ENTRYPOINT ["gnuplot"]
```

and save it, and then again in the shell (one command at a time!):

```
sudo docker build -t gnuplot_centos .
rm ~/input/pm3d_lighting.2.png
sudo docker run --name DockerGNUPlot -v ~/input:/workdir gnuplot_centos pm3d_lighting.2.gnu
ls ~/input
sudo docker image save -o gnuplotCentosDemo.tar gnuplotcentos
sudo docker image import gnuplotCentosDemo.tar importedgnuplot
sudo docker image list
```
