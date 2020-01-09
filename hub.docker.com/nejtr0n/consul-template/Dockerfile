FROM gliderlabs/alpine:latest
MAINTAINER Jimmy Nejtr0n <a6y@xakep.ru>
ENV CONSUL_TEMPLATE_VERSION 0.14.0
ADD https://releases.hashicorp.com/consul-template/${CONSUL_TEMPLATE_VERSION}/consul-template_${CONSUL_TEMPLATE_VERSION}_linux_amd64.zip /
RUN unzip consul-template_${CONSUL_TEMPLATE_VERSION}_linux_amd64.zip  
RUN mv consul-template /usr/local/bin/consul-template 
RUN rm -rf /consul-template_${CONSUL_TEMPLATE_VERSION}_linux_amd64.zip 

CMD [ "/usr/local/bin/consul-template"]
