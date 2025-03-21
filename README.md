## Zoneminder Docker for phusion/baseimage:focal-1.2.0

(Zoneminder version: 1.36)

### About
This is an easy to run dockerized image of [ZoneMinder](https://github.com/ZoneMinder/zoneminder) along with the the [ZM Event Notification Server](https://github.com/pliablepixels/zmeventnotification).  

The configuration settings that are needed for this implementation of Zoneminder are pre-applied and do not need to be changed on the first run of Zoneminder.

This verson will now upgrade from previous versions of Zoneminder.

As this repository is a Fork of the DLANDON repository I will keep the donation link below:  
You can donate [here](https://www.paypal.com/us/cgi-bin/webscr?cmd=_s-xclick&amp;hosted_button_id=EJGPC7B5CS66E).

#### Components
- base image: phusion/baseimage:focal-1.2.0
- Mail client : ssmtp
- webserver : apache2 (ppa:ondrej/apache2)
- Webcode : PHP7.4 (ppa:ondrej/php)
- Database : mariadb (latest)
- Zoneminder 1.36

Total size of the container at deployement is 473 MB. 

### Deployment
Easiest way to deploy is doing the following:  
- ssh to your Docker host (AMD64 machine only)
- create a new directory somewhere on this machine (assert /opt/zoneminder2025)
- create a new file here, named docker-compose.yml and take over the contents of the file inside this repo.
- make Docker pull this git repository: (we use `zoneminder2025 ` as a image reference, you can change it to whatever you like) 
- ```docker build -t zoneminder2025 github.com/infinity202/zoneminder.phusion ```
- building the first time will take several minutes !
- when finished:
- ```sudo docker compose -f docker-compose.yaml up```
- Your Zoneminder server will be up in a few minutes and reachable on https://`your docker host`:8843/zm
- the ports are defined in your docker-compose.yml file! !

#### Usage

To access the Zoneminder gui, browse to: `https://<your host ip>:8443/zm` or `http://<your host ip>:8080/zm` if `-p 8080:80/tcp` is specified.

The zmNinja Event Notification Server is accessed at port `9000`.  Security with a self signed certificate is enabled.  You may have to install the certificate on iOS devices for the event notification to work properly.

#### Troubleshooting when the docker fails

If you have a situation where the docker fails to start, you can set an environemtnt variable when the docker is started and MySql and Zoneminder will not be started.  This will keep the docker running so you can get into a command line in the docker and troubleshoot the problem.

Create an environment variable:
NO_START_ZM="1"

MySql and Zoneminder will not be started.

Get into a command line in the docker and troubleshoot your issue by using the following commands to start MySql and zonemonder and fix any errors/problems with them starting.

service mysql start

service zoneminder start
