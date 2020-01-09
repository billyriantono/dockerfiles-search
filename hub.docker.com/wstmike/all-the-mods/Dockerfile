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

RUN wget -O AllTheMods.zip --no-check-certificate https://minecraft.curseforge.com/projects/all-the-mods-3/files/2583612/download && \
	unzip AllTheMods.zip && \
	rm AllTheMods.zip

# Creating user and downloading files
RUN chmod u+x startserver.sh && \
	echo "#By changing the setting below to TRUE you are indicating your agreement to our EULA (https://account.mojang.com/documents/minecraft_eula)." > eula.txt && \
	echo "$(date)" >> eula.txt && \
	echo "eula=TRUE" >> eula.txt

# Expose port 25565
EXPOSE 25565

# Expose volume
VOLUME ["/minecraft/world"]

# Start server
CMD ["/bin/bash", "/minecraft/startserver.sh"]