# Container for CTFs and infosec
FROM kalilinux/kali-linux-docker

MAINTAINER dev@sprico.com

ENV CTF_USER ctf
ENV CTF_PASSWD ctf

RUN apt update && apt upgrade -y
RUN apt install metasploit-framework tmux -y

RUN msfdb init

# create ctf user
RUN useradd -m $CTF_USER
RUN usermod -aG sudo $CTF_USER
RUN echo "$CTF_USER:$CTF_PASSWD" | chpasswd
USER ctf

WORKDIR /home/ctf
ENTRYPOINT service postgresql start
