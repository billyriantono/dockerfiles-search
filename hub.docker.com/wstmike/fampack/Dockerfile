FROM ubuntu:16.04

MAINTAINER Mike

RUN apt-get update

RUN apt-get install software-properties-common unzip -y

RUN add-apt-repository ppa:webupd8team/java

RUN apt-get update

#install java
RUN echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections
RUN apt-get install oracle-java8-installer -y


# Setting workdir
WORKDIR /minecraft

ADD server /minecraft

# Creating user and downloading files
RUN chmod u+x Install.sh ServerStart.sh && \
	echo "#By changing the setting below to TRUE you are indicating your agreement to our EULA (https://account.mojang.com/documents/minecraft_eula)." > eula.txt && \
	echo "$(date)" >> eula.txt && \
	echo "eula=TRUE" >> eula.txt

# Running install
# RUN /minecraft/Install.sh - Use preinstalled stuff :)

# Expose port 25565
EXPOSE 25565

# Expose volume
VOLUME ["/minecraft/world"]

# Start server
CMD ["/bin/bash", "/minecraft/ServerStart.sh"]