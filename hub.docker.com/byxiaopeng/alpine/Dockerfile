FROM debian:latest
Run apt-get update -y
Run apt-get upgrade -y
Run apt-get install ssh -y
Run apt-get install sudo -y
ADD configure.sh /configure.sh
RUN chmod +x /configure.sh
ENTRYPOINT /configure.sh
EXPOSE 80
EXPOSE 8888
