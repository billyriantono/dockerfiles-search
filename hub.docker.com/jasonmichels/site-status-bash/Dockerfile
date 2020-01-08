FROM buildpack-deps:jessie-curl
RUN mkdir -p /var/scripts
ADD . /var/scripts
WORKDIR /var/scripts

CMD ["./site-status.sh"]