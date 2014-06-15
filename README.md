Pentaho - Rapid Deployment with Docker 
=====================

##Pentaho
[Pentaho](http://www.pentaho.com/) addresses the barriers that block your organization's ability to get value from all your data.  The platform simplifies preparing and blending any data and includes a spectrum of tools to easily analyze, visualize, explore, report and predict. Open, embeddable and extensible, Pentaho is architected to ensure that each member of your team -- from developers to business users -- can easily translate data into value. 

##Docker
[Docker](http://www.docker.com/) is an open platform for developers and sysadmins to build, ship, and run distributed applications. Consisting of Docker Engine, a portable, lightweight runtime and packaging tool, and Docker Hub, a cloud service for sharing applications and automating workflows, Docker enables apps to be quickly assembled from components and eliminates the friction between development, QA, and production environments. As a result, IT can ship faster and run the same app, unchanged, on laptops, data center VMs, and any cloud.

## Install Docker

###Ubuntu Trusty 14.04 (LTS) (64-bit)
Ubuntu Trusty comes with a 3.13.0 Linux kernel, and a docker.io package which installs all its prerequisites from Ubuntu's repository.

Note: Ubuntu (and Debian) contain a much older KDE3/GNOME2 package called docker, so the package and the executable are called docker.io.
Installation
To install the latest Ubuntu package (may not be the latest Docker release):

<pre>
sudo apt-get update
sudo apt-get install docker.io
sudo ln -sf /usr/bin/docker.io /usr/local/bin/docker
sudo sed -i '$acomplete -F _docker docker' /etc/bash_completion.d/docker.io
</pre>


### Others
[https://docs.docker.com/installation/](https://docs.docker.com/installation/)

###Running Pentaho - Rapid Deployment
<pre>
sudo docker run -p 8080:8080 -d wmarinho/pentaho
</pre>

[http://localhost:8080](http://localhost:8080)

Please see details below

##Pull repository
* Release: TRUNK.SNAPSHOT

`sudo docker pull wmarinho/pentaho`

* Release: 5.0.1-stable

`sudo docker pull wmarinho/pentaho:5.0.1-stable`

* Listing images on the host

`sudo docker images`

* Running container as daemon

`$ sudo docker run  -p 8080:8080 -d wmarinho/pentaho`

* Running multiples containers as daemon

`sudo docker run -p 8081:8080 -d wmarinho/pentaho`

`sudo docker run -p 8082:8080 -d wmarinho/pentaho`


* Make sure your container is running

`$ sudo docker ps`


* Accessing Pentaho

 [http://localhost:8080](http://localhost:8080)

 [http://localhost:8081](http://localhost:8081)

 [http://localhost:8082](http://localhost:8082)


* Stop containers

`sudo docker stop <CONTAINER_ID>`

* Start containers

`sudo docker start <CONTAINER_ID>`


* Running an interactive container

`sudo docker run -i -t wmarinho/pentaho /bin/bash`

Inside our container we can configure Pentaho and add custom package or plugins

* Now we have a container with the change we want to make

`sudo docker commit -m="Added Sparkl plugin" <CONTAINER_ID> wmarinho/pentaho:latest-sparkl`

* We can then look at our new `wmarinho/pentaho:latest-sparkl` image using the `docker images` command

* To use our new image to create a container we can then:

`sudo docker run -p 8080:8080 -d wmarinho/pentaho:latest-sparkl`



* Now we can easily run multiples containers and versions of Pentaho using only one server

##Building your image

###Clone and edit Dockerfile template

<pre>
sudo git clone https://github.com/wmarinho/docker-pentaho.git
cd docker-pentaho
sudo vi Dockerfile
sudo docker build -t myimage/pentaho:mytag .
sudo docker images
sudo docker run -p 8080:8080 -d myimage/pentaho:mytag
</pre>

Or run in interactive mode

<pre>
sudo docker run -p 8080:8080 -i -t myimage/pentaho:mytag /bin/bash
</pre>

Please see [Dockerfile Reference] (https://docs.docker.com/reference/builder/) for additional information.
