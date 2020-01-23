FROM debian:latest
COPY fixed.deb /tmp
RUN apt update && apt upgrade -y
RUN apt install -y /tmp/fixed.deb 

CMD /opt/1C/licence/3.0/licenceserver -r

