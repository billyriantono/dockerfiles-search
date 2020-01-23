FROM    debian:jessie

MAINTAINER yukikaze/gn64

RUN echo "deb http://ftp.debian.org/debian testing main contrib non-free\ndeb http://ftp.debian.org/debian/ jessie-updates main contrib non-free\ndeb http://security.debian.org/ jessie/updates main contrib non-free" > /etc/apt/source.list && \
apt-get update -y && apt-get install -y --no-install-recommends locales apt-utils && \
apt-get clean && \
echo en_US.UTF-8 UTF-8 > /etc/locale.gen && \
locale-gen && \
update-locale LANG=en_US.UTF-8 && \
apt-get -y install tar wget at sudo imagemagick graphicsmagick poppler-utils libjpeg-progs \
python2.7 python-requests python-docopt python-crypto python-pillow python-sqlalchemy python-anyjson \
python-simplejson python-paste openjdk-7-jre-headless && apt-get clean

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8
RUN groupadd libre10 && useradd -g libre10 libre10 && \
wget https://bitbucket.org/gn64/libre10/get/1.5.2.tar.gz && tar xvzf 1.5.2.tar.gz && \
python2 ./gn64-libre10-ac8271735f60/www/libre10_exec.py install && \
rm -rf ./gn64-libre10-ac8271735f60 && rm -f ./1.5.2.tar.gz && \
chown -R libre10:libre10 /var/www/libre10 && chown -R libre10:libre10 /opt/libre10 && \
chmod 777 /usr/local/bin/libre10*

EXPOSE 8008:8008
EXPOSE 8983

CMD /bin/bash -c "atd&sudo -u libre10 /bin/bash -c 'export PATH=$PATH:/usr/local/bin && libre10-wsgi& sleep 5; export PATH=$PATH:/usr/local/bin && cd /opt/libre10/solr/example && java -jar start.jar& sleep 30 && /usr/local/bin/libre10 update && sleep 10 && /usr/local/bin/libre10 import && /bin/bash'"