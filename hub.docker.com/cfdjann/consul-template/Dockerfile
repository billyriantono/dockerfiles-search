FROM cfdjann/base
MAINTAINER JSK

ADD https://github.com/hashicorp/consul-template/releases/download/v0.3.1/consul-template_0.3.1_linux_amd64.tar.gz /tmp/consul-template.tar.gz

RUN cd /bin && gzip -dc /tmp/consul-template.tar.gz | tar -xf - && rm /tmp/consul-template.tar.gz && mv /bin/consul-template_0.3.1_linux_amd64/consul-template /bin/consul-template && rmdir /bin/consul-template_*

CMD ["/bin/consul-template"]