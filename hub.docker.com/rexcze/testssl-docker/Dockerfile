FROM ubuntu:yakkety

ENV TESTSSLVERSION="v2.8rc3" 

RUN apt-get update && apt-get install -y --no-install-recommends bsdmainutils ca-certificates curl dnsutils git aha python3 python3-pip gcc libc6-dev make perl zlib1g-dev python3-setuptools nginx supervisor\
	&& apt-get clean

RUN pip3 install wheel
RUN pip3 install Flask

RUN cd /usr/local/bin/ && git clone https://github.com/TKCERT/testssl.sh-webfrontend.git

RUN git clone -b ${TESTSSLVERSION} --single-branch https://github.com/drwetter/testssl.sh.git /usr/local/bin/testssl.sh-webfrontend/testssl.sh/

COPY files/docker-testssl.conf /etc/nginx/sites-enabled/docker-testssl.conf

RUN rm -f /etc/nginx/sites-enabled/default

RUN mkdir -p /testssl.sh && ln -s /usr/local/bin/testssl.sh-webfrontend/testssl.sh/testssl.sh /testssl.sh/testssl.sh

COPY files/sup-nginx.conf /etc/supervisor/conf.d/sup-nginx.conf

EXPOSE 80

ENTRYPOINT ["/usr/bin/supervisord"]
CMD ["-n"]
