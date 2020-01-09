FROM ubuntu:16.04
RUN sed -i -e s/archive.ubuntu.com/mirror.kku.ac.th/g /etc/apt/sources.list
RUN apt-get update && apt-get install -y openssh-server && apt-get clean
RUN sed -i -e s/prohibit-password/yes/g /etc/ssh/sshd_config
COPY docker-entrypoint.sh /docker-entrypoint.sh
RUN chmod 755 /docker-entrypoint.sh
EXPOSE 22
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["/bin/bash"]
