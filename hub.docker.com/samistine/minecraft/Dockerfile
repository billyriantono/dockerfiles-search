FROM nimmis/java:openjdk-8-jdk

MAINTAINER Samuel Seidel <samuel@samistine.com>

# Default TimeZone
ENV TZ America/New_York

# Fix timezone
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Java options for Minecraft server
ENV MC_JAVA_OPS '-Xmx1G -Xms1G'

# add extra files needed
COPY rootfs /

# Make special user for minecraft to run in
RUN useradd -s /bin/bash -d /minecraft -m minecraft

# expose minecraft port
EXPOSE 25565
