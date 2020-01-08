FROM quxz/ubuntu_systemd:latest
RUN apt-get install apache2 -y && apt-get install libapache2-mod-wsgi-py3 -y
EXPOSE 80
VOLUME ["/sys/fs/cgroup"]
CMD ["apache2ctl","-D","FOREGROUND"]