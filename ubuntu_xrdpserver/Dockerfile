FROM ubuntu
MAINTAINER David Gey
RUN apt-get -y update
# Install base system
RUN apt-get -y install --no-install-recommends xrdp

EXPOSE 3389
ENTRYPOINT /etc/init.d/xrdp start && /bin/bash
