FROM ubuntu
MAINTAINER David Gey
#ENV http_proxy=http://192.168.2.101:8888/
RUN apt-get -y update
# Install base system
RUN apt-get -y install --no-install-recommends ubuntu-desktop gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal tightvncserver xrdp
# Install additional software
RUN apt-get -y install git firefox libreoffice wget

RUN sed -i '$ d' /etc/xrdp/startwm.sh && \
 echo 'gnome-panel & \ngnome-settings-daemon & \nmetacity & \nnautilus &' >> /etc/xrdp/startwm.sh && \
 cat /etc/xrdp/sesman.ini | sed -e '/localhost/d' | sed -e 's/ListenAddress=127.0.0.1/ListenAddress=0.0.0.0/g' > /etc/xrdp/sesman.ini && \
 useradd vnc -s /bin/bash &&  adduser vnc sudo && mkdir -p /home/vnc/.vnc && chown -R vnc /home/vnc/.vnc && chown -R vnc /home/vnc && \
 sed -i '$ d' /etc/shadow  && echo 'vnc:$6$iG6ExtJl$lxJVKq0BtWS786dSrd8/hAX8/Dk08fqavmsAS4j3MvAzjLnw.2eVdkUH5wfTx44eyavr/rLr7786CXwemL8Dr0:16840:0:99999:7:::' >> /etc/shadow && \
 echo "postbank123" | vncpasswd -f > /home/vnc/.vnc/passwd && \
 echo 'gnome-session' > /home/vnc/.xsession && \
 echo 'export JAVA_HOME=/software/jdk\nexport M2_HOME=/software/maven\nexport PATH=$M2_HOME/bin:$JAVA_HOME/bin:$PATH' > /etc/profile && \
 echo '#!/bin/bash \n\nunset SESSION_MANAGER\n\ngnome-panel &\ngnome-settings-daemon &\nmetacity & \nnautilus &' > /home/vnc/.vnc/xstartup ; chmod 755 /home/vnc/.vnc/xstartup

ADD sesman.ini /etc/xrdp

#VOLUME /home/vnc

# Patching in a newer version of xrdp since version 0.6.0 in Ubuntu 14.04 has a bug which does not allow to reuse open sessions
ADD xrdp_0.6.1-2_amd64.deb /var/tmp
RUN dpkg -i /var/tmp/xrdp_0.6.1-2_amd64.deb

ADD *.desktop /usr/share/applications

EXPOSE 3389 5901
ENTRYPOINT /etc/init.d/xrdp start && /bin/bash
