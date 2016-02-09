FROM ubuntu
MAINTAINER David Gey
RUN apt-get -y update
# Install base system
RUN apt-get -y install --no-install-recommends ubuntu-desktop gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal tightvncserver xrdp
# Install additional software
RUN apt-get -y install git firefox libreoffice

RUN sed -i '$ d' /etc/xrdp/startwm.sh
RUN echo 'gnome-panel & \ngnome-settings-daemon & \nmetacity & \nnautilus &' >> /etc/xrdp/startwm.sh

RUN useradd vnc -s /bin/bash ;  adduser vnc sudo ; mkdir -p /home/vnc/.vnc ; chown -R vnc /home/vnc/.vnc ; chown -R vnc /home/vnc
RUN echo 'vnc:postbank123' | chgpasswd 
RUN echo "postbank123" | vncpasswd -f > /home/vnc/.vnc/passwd
RUN echo 'gnome-session' > /home/vnc/.xsession
RUN echo '#!/bin/bash \n\nunset SESSION_MANAGER\n\ngnome-panel &\ngnome-settings-daemon &\nmetacity & \nnautilus &' > /home/vnc/.vnc/xstartup ; chmod 755 /home/vnc/.vnc/xstartup

#VOLUME /home/vnc

EXPOSE 3389
EXPOSE 5901
ENTRYPOINT /etc/init.d/xrdp start && /bin/bash
