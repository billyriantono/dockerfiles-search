FROM assembla/ubuntu
MAINTAINER Artiom Di <kron82@gmail.com>

RUN apt-get install -y memcached
EXPOSE 11211
CMD ["memcached", "-u", "root", "-v"]
