FROM alpine:3.3

MAINTAINER DevOps "devops@airhelp.com"

RUN apk --update --no-cache add ca-certificates

RUN wget -O /tmp/consul-template.zip https://releases.hashicorp.com/consul-template/0.15.0/consul-template_0.15.0_linux_amd64.zip && \
	unzip /tmp/consul-template.zip -d /usr/local/bin/ && \
	rm /tmp/consul-template.zip && \
	mkdir /templates /output

VOLUME ["/templates", "/output"]

ENTRYPOINT ["consul-template"]
