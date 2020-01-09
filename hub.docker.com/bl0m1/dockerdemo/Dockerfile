FROM ubuntu:16.04
MAINTAINER Hugo Blom hugo.blom1@gmail.com

#update and install packages
RUN \
 echo "**** install packages ****" && \
 apt-get update && \
 apt-get install -y \
  sudo \
  unzip \
  man-db \
  curl

#set workdir and copy .sh
WORKDIR /rclone
COPY run-me.sh /rclone/

#make .sh executeble
RUN chmod +x /rclone/run-me.sh

ENTRYPOINT ["/rclone/run-me.sh"]
