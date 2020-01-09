FROM docker:18.09

RUN apk --no-cache add curl bash openssl openssh-client python

# install rdocker script
COPY rdocker.sh /usr/local/bin/rdocker
RUN chmod +x /usr/local/bin/rdocker

CMD ["rdocker"]

# labels for https://microbadger.com/ service
LABEL org.label-schema.vcs-url="https://bitbucket.org/senofi/remote-docker"
