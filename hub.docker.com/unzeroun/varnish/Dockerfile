FROM unzeroun/base


RUN curl https://repo.varnish-cache.org/GPG-key.txt | apt-key add -
RUN echo "deb https://repo.varnish-cache.org/debian/ jessie varnish-4.0" >> /etc/apt/sources.list.d/varnish-cache.list

RUN aptitude update
RUN aptitude install -y varnish

ADD default.vcl /etc/varnish/default.vcl

EXPOSE 80

ENTRYPOINT ["varnishd"]
CMD ["-a", "0.0.0.0:80", "-f", "/etc/varnish/default.vcl", "-F", "-s", "malloc,128m"]
