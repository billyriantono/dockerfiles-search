FROM twdevops/base
MAINTAINER ShawnMa <qsma@thoughtworks.com>

## Add repository
RUN \
  apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 7BD9BF62 &&\
  echo "deb http://nginx.org/packages/ubuntu trusty nginx" > /etc/apt/sources.list.d/nginx.list

## Install packages
RUN \
  apt-get update &&\
  apt-get install -y --no-install-recommends nginx &&\
  wget -P /usr/local/bin https://godist.herokuapp.com/projects/ddollar/forego/releases/current/linux-amd64/forego && chmod u+x /usr/local/bin/forego

## Install docker-gen
RUN \
  wget https://github.com/jwilder/docker-gen/releases/download/0.3.9/docker-gen-linux-amd64-0.3.9.tar.gz &&\
  tar -C /usr/local/bin -xvzf docker-gen-linux-amd64-0.3.9.tar.gz &&\
  rm /docker-gen-linux-amd64-0.3.9.tar.gz

## Install scripts
ADD entrypoint.sh /entrypoint.sh
RUN chmod a+x     /entrypoint.sh

## Install templates
ADD  files/nginx.tmpl /app/

## Cleanup
RUN \
  apt-get autoclean -y &&\
  apt-get autoremove -y &&\
  rm -rf /tmp/*  &&\
  rm -rf /var/tmp/* &&\
  rm -rf /var/lib/apt/lists/*

WORKDIR /app/

EXPOSE 80 443

ENTRYPOINT ["/entrypoint.sh"]

VOLUME ["/var/lib/nginx"]

CMD ["nginx", "-g", "daemon off;"]
