FROM ubuntu:latest

RUN apt-get update && apt-get dist-upgrade -y && apt-get install openssh-server -y

RUN apt-get install psmisc htop vim gcc-6-base -y

# delete all the apt list files since they're big and get stale quickly
RUN rm -rf /var/lib/apt/lists/*

# enable the universe
RUN sed -i 's/^#\s*\(deb.*universe\)$/\1/g' /etc/apt/sources.list

CMD ["/bin/bash"]
