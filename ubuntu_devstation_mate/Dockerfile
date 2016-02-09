FROM ubuntu
MAINTAINER David Gey
RUN apt-get -y install software-properties-common
RUN apt-add-repository -y ppa:ubuntu-mate-dev/ppa
RUN apt-add-repository -y ppa:ubuntu-mate-dev/trusty-mate
RUN apt-get -y update && apt-get -y upgrade
# Install base system
RUN apt-get -y install --no-install-recommends xrdp ubuntu-mate-core ubuntu-mate-desktop
# Install additional software
#RUN apt-get -y install git firefox libreoffice

EXPOSE 3389
EXPOSE 5901
ENTRYPOINT /etc/init.d/xrdp start && /bin/bash
