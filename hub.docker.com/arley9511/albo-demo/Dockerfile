FROM google/cloud-sdk:alpine

RUN apk update && apk add bash

RUN apk add maven gettext

RUN apk --no-cache add openjdk11 --repository=http://dl-cdn.alpinelinux.org/alpine/edge/community

RUN gcloud components install kubectl

COPY pipe.sh /

ENTRYPOINT ["/pipe.sh"]
