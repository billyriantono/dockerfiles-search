FROM alleotech/php-fpm:7.1

LABEL org.label-schema.schema-version="1.0" \
    org.label-schema.name="SSHd Docker Image" \
    org.label-schema.vendor="AlleoTech Ltd" \
    org.label-schema.livence="MIT" \
    org.label-schema.build-data="2019052401"

MAINTAINER AlleoTech <admin@alleo.tech>

RUN yum -y install --setopt=tsflags=nodocs openssh-server \
    && yum clean all \
    && rm -rf /var/cache/yum \
    && mkdir /root/.ssh \
    && chmod 0700 /root/.ssh \
    && rm -f /root/anaconda-ks.cfg

COPY run.sh /usr/local/bin/run.sh
EXPOSE 22

CMD ["/usr/local/bin/run.sh"]
