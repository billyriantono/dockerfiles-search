FROM miko2u/nginx
MAINTAINER miko@cafelounge.net

RUN cd /usr/local \
 && yum -y install git python python-devel python-virtualenv \
     gcc dialog augeas-libs openssl-devel libffi-devel \
     redhat-rpm-config ca-certificates \
 && git clone https://github.com/letsencrypt/letsencrypt \
 && ln -s /usr/local/letsencrypt/letsencrypt-auto /usr/local/bin/letsencrypt-auto \
 && ln -s /usr/local/letsencrypt/bootstrap /usr/local/bin/bootstrap \
 && letsencrypt-auto --help \
 && rm -rf /var/tmp/* /var/lib/yum/* /var/cache/yum/*

# configure
COPY *.conf /etc/nginx/conf.d/
COPY *.crt /etc/pki/tls/certs/

# init
COPY init /boot/
ENTRYPOINT ["/boot/init"]

# overlap commands
EXPOSE 8844
CMD ["letsencrypt-auto","--help"]
