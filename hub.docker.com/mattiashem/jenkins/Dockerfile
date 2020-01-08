FROM jenkins
# if we want to install via apt
USER root
RUN apt-get update 
RUN apt-get install apt-transport-https ca-certificates apt-utils -y
RUN apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
RUN  echo "deb https://apt.dockerproject.org/repo debian-jessie main" >> /etc/apt/sources.list.d/docker.list
RUN cat /etc/apt/sources.list.d/docker.list
RUN apt-get update
RUN apt-get update && apt-get install sudo  fabric rsync docker-engine -y
RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers
USER jenkins 
