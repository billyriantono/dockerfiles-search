FROM samueldebruyn/debian-git
MAINTAINER smheidrich

ENV DEBIAN_FRONTEND noninteractive

# install sshd
RUN apt-get -y update && apt-get -y install openssh-server

# slim down image
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/man/?? /usr/share/man/??_*
