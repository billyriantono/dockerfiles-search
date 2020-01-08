FROM anapsix/alpine-java

#Installs Curl
RUN apk update && apk add \
curl

#Exports Path
RUN export MINEPATH="/usr/minecraft"

#Makes Minecraft Dir
RUN mkdir /usr/minecraft

#Get Minecraft Server Jar
RUN curl -sSL https://launcher.mojang.com/v1/objects/fe123682e9cb30031eae351764f653500b7396c9/server.jar -o /usr/minecraft/server.jar

#Tests to see if the file is there
RUN ls -l /usr/minecraft

#Runs server to generate eula
RUN java -Xms512M -Xmx2048M -jar /usr/minecraft/server.jar nogui
RUN sed -i 's/false/true/g' eula.txt

#Exposes the ports need for the server
EXPOSE 25565/tcp
EXPOSE 25565/udp

#Runs server completed
RUN echo "java -jar /usr/minecraft/server.jar -Xms512m -Xmx2g nogui" > /usr/minecraft/script.sh
#RUN chmod +x /usr/minecraft/script.sh
ENTRYPOINT ["/bin/sh", "/usr/minecraft/script.sh"]
