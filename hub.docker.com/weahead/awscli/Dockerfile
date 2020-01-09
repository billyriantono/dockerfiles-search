FROM alpine:3.6

LABEL maintainer="We ahead <docker@weahead.se>"

RUN adduser -h /home/aws -g '' -s /bin/false -D aws

ENV AWS_CLI_VERSION=1.11.177\
		PYTHONIOENCODING=UTF-8\
		PAGER=cat

RUN apk --no-cache add \
			ca-certificates \
			groff \
			python2 \
			py2-pip \
		&& pip --no-cache-dir install awscli==${AWS_CLI_VERSION}

USER aws

ENTRYPOINT ["/usr/bin/aws"]
