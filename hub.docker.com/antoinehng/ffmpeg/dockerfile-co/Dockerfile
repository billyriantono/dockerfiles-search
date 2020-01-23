FROM centos:centos7

MAINTAINER anti1346 <anti1346@gmail.com>

#RUN sed -i 's/enabled\=1/enabled\=0/g' /etc/yum/pluginconf.d/fastestmirror.conf \
#  && echo "sslverify=false" >> /etc/yum.conf
RUN yum install -y yum-plugin-fastestmirror
RUN yum install -y epel-release \
  && yum -y update \
  && yum install -y bind bind-export-libs bind-utils iproute \
  && yum install -y procps net-tools wget vim whicha \
  && yum clean all \
  && rm -rf /root/.cache 

RUN cat /usr/share/zoneinfo/Asia/Seoul > /etc/localtime

RUN mkdir -p /data/named/{conf,zonefile,log}
#RUN mkdir -p /var/named/{masters,slaves}

COPY ./docker_src /src
RUN cp /src/named.ca /var/named/named.ca \
  && cp /src/named.conf /data/named/conf/named.conf \
  && cp /src/named.rfc1912.zones /data/named/conf/named.rfc1912.zones \
  && cp /src/named.logging.conf /data/named/conf/named.logging.conf \
  && cp /src/example.dns.zone /data/named/zonefile/example.dns.zone

RUN chown -R named:named /data/named \
  && chown -R named:named /var/named

#RUN rndc-confgen -b 512 -u named -k rndc-key -p 953 -s 0.0.0.0 > /etc/rndc.conf
RUN rndc-confgen -a -c /etc/rndc.key \
  && chown named:named /etc/rndc.key

RUN chmod 755 /src/entrypoint.sh

RUN echo 'export PS1="\[\e[31m\]\u\[\e[m\]\[\e[37m\]@\[\e[m\]\[\e[96m\]\h\[\e[m\]:\[\033[01;93m\]\W\[\e[m\]$ "' >> /root/.bashrc

EXPOSE 53/udp 53/tcp 953/tcp

ENTRYPOINT ["/src/entrypoint.sh"]

CMD ["/usr/sbin/named"]
