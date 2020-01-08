FROM hashicorp/terraform:light

MAINTAINER "Chris McKee <pcdevils@gmail.com>"

RUN apk add --update git bash

ADD docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh

RUN adduser -S tf-cli
USER tf-cli

ENTRYPOINT ["/docker-entrypoint.sh"] 

WORKDIR "/tf-cli"

# Executing defaults
CMD ["/bin/sh"]
