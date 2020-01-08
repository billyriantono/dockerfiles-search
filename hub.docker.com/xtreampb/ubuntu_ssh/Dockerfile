FROM ubuntu:latest
LABEL maintainer="chris.thomas@clear-measure.com"

RUN apt-get update
RUN apt-get install ssh -y
RUN apt-get upgrade -y
RUN apt-get clean -y

COPY docker_ssh_startup.sh /bin/ssh_startup.sh
RUN sed -i 's/\r//' /bin/ssh_startup.sh
RUN chmod 755 /bin/ssh_startup.sh
RUN echo ssh_startup.sh >> /root/.bashrc
