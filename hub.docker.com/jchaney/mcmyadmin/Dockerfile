FROM        java:7u65
MAINTAINER  Josh Chaney "josh@chaney.io"

# Add minecraft user
RUN         useradd minecraft -m -s /bin/bash

# Install McMyAdmin
ADD         etc.zip /usr/local/
WORKDIR     /usr/local
RUN         unzip etc.zip && \
            rm etc.zip
ADD         MCMA2_glibc26_2.zip /home/minecraft/mcmyadmin/
WORKDIR     /home/minecraft/mcmyadmin
RUN         unzip MCMA2_glibc26_2.zip && \
            rm MCMA2_glibc26_2.zip && \
            ./MCMA2_Linux_x86_64 -nonotice -updateonly

# Fix Permissions
RUN         chown -R minecraft:minecraft /home/minecraft

# Open ports
EXPOSE      8080
EXPOSE      25565

# Change user
USER        minecraft

ENTRYPOINT  ["/home/minecraft/mcmyadmin/MCMA2_Linux_x86_64"]
CMD	    ["-setpass", "pass123"]
