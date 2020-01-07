FROM ubuntu:19.04

ENV TEMP_DEB=temp.deb

RUN apt-get upgrade && apt-get update
RUN apt-get update && apt-get install -y wget python libpython2.7

### setup mysql-shell
RUN wget -O "$TEMP_DEB" "https://dev.mysql.com/get/Downloads/MySQL-Shell/mysql-shell_8.0.17-1ubuntu19.04_amd64.deb"
RUN dpkg -i "$TEMP_DEB"
RUN rm -f "$TEMP_DEB"
