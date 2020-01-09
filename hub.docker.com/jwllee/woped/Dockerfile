# WoPed 3.7.1
#
# Example usage:
# docker run -d \
# 		 -v /etc/localtime:/etc/localtime:ro \
# 		 -v /tmp/.X11-unix:/tmp/.X11-unix \
# 		 -v $HOME/woped:/home/woped/data \
# 		 -e DISPLAY=unix$DISPLAY \
# 		 --device /dev/snd:/dev/snd \
# 		 --name woped \
# 		 woped:latest
FROM ubuntu:18.04
LABEL maintainer "Wai Lam Jonathan Lee <jonathan.wailam.lee@gmail.com>"
LABEL description="WoPeD (Workflow Petri Net Designer)"

# to get add-apt-repository
RUN apt-get update && apt-get install -y \
	software-properties-common 

# Installing Oracle Java 8, has to be this one! or else you get errors
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections \
	&& add-apt-repository -y ppa:webupd8team/java \
	&& apt-get update && apt-get install -y \
	oracle-java8-installer \
	&& rm -rf /var/lib/apt/lists/* \
	&& rm -rf /var/cache/oracle-jdk8-installer

# Packages needed to run WoPeD
RUN apt-get update && apt-get install -y \
	libxext6 \
	libxrender1 \
	libxtst6 \
	libxi6 \
	wget 

ENV HOME /home/woped

WORKDIR $HOME

RUN useradd --create-home --home-dir $HOME woped \
	&& groupadd app \
	&& gpasswd -a woped app \
	&& chown -R woped:woped $HOME

# RUN wget https://sourceforge.net/projects/woped/files/woped/3.7.1/WoPeD-install-linux-3.7.1.jar
COPY WoPeD/ $HOME/app/
WORKDIR $HOME/app
USER woped

ENTRYPOINT [ "java", "-jar", "WoPeD.jar" ]
