FROM gocd/gocd-agent-docker-dind:v18.7.0
# Install make
RUN apk add --update alpine-sdk
# Install docker-compose
RUN apk add --no-cache py-pip && pip install docker-compose

ADD gocd-entrypoint.sh / 
RUN chmod +x /gocd-entrypoint.sh

ENTRYPOINT ["/gocd-entrypoint.sh"]