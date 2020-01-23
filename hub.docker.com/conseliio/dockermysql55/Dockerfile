FROM mysql:5.5

RUN  echo "Europe/Paris" > /etc/timezone
RUN  dpkg-reconfigure -f noninteractive tzdata
CMD ["mysqld"]
