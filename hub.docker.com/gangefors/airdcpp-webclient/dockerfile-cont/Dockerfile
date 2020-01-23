FROM crosbymichael/java

ADD https://s3.amazonaws.com/Minecraft.Download/versions/1.8.4/minecraft_server.1.8.4.jar /minecraft.jar 
RUN chown 1000:1000 /minecraft.jar && mkdir /minecraft && chown 1:1 /minecraft

WORKDIR /minecraft
USER 1000

ENTRYPOINT ["java"]
CMD ["-Xmx1536M", "-Xms768M", "-jar", "/minecraft.jar", "nogui"]
