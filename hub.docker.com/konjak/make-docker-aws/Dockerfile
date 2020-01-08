FROM docker:latest
RUN apk --no-cache add bash git util-linux coreutils gettext grep jq make bash-completion py-pip groff \
 && pip install docker-compose \
 && pip install awscli
COPY versions.sh /usr/local/bin/
ENTRYPOINT [""]
