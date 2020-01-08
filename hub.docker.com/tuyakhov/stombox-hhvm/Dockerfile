#########################################################################
#
# A Stombox HHVM container - used by our API
#
# Build with:
#  docker build -t="tuyakhov/stombox-hhvm" .
#
#
########################################################################

# Base from official ubuntu image
FROM ubuntu:trusty

#### Install HHVM
RUN apt-get install -y wget
RUN wget -O - http://dl.hhvm.com/conf/hhvm.gpg.key | apt-key add -
RUN echo deb http://dl.hhvm.com/ubuntu trusty main | tee /etc/apt/sources.list.d/hhvm.list
RUN apt-get update && apt-get install -y hhvm hhvm-dev
# Running command-line scripts with HHVM for /usr/bin/php
RUN /usr/bin/update-alternatives --install /usr/bin/php php /usr/bin/hhvm 60

### Install required HHVM extenstion
RUN apt-get install -y --force-yes git-core \
    automake \
    autoconf \
    libtool \
    gcc \
    build-essential

RUN wget https://s3.amazonaws.com/drivers.mongodb.org/hhvm/hhvm-mongodb-1.0beta1.tgz \
    && tar -xvzf ../hhvm-mongodb-1.0beta1.tgz \
    && cd hhvm-mongodb-1.0beta1 \
    && hphpize \
    && cmake . && make configlib \
    && make -j 16 && make install
RUN mkdir /etc/hhvm/extensions && sudo mv /hhvm-mongodb-1.0beta1/mongodb.so /etc/hhvm/extensions
RUN echo "hhvm.dynamic_extension_path=/etc/hhvm/extensions" >> /etc/hhvm/php.ini
RUN echo "hhvm.dynamic_extensions[mongodb]=mongodb.so" >> /etc/hhvm/php.ini

CMD hhvm --mode server -v Server.Type=fastcgi -v Server.Port=9000

VOLUME ["/var/log/hhvm"]
