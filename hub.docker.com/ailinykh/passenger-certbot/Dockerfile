FROM phusion/passenger-ruby23

RUN apt-get install software-properties-common &&\
    gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 75BCA694 &&\
    # add-apt-repository ppa:certbot/certbot &&\
    apt-get update &&\
    apt-get install python-certbot-nginx -y

CMD ["/sbin/my_init"]
