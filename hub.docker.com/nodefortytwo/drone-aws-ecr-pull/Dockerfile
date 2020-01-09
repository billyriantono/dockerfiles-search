FROM mesosphere/aws-cli

RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories
RUN apk update 
RUN apk add docker

ADD ./scripts/ecr-pull /bin

RUN chmod a+x /bin/ecr-pull

ENTRYPOINT /bin/ecr-pull