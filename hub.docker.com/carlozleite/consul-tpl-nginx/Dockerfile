FROM nginx:stable-alpine

RUN apk upgrade --update-cache --available
RUN apk add supervisor wget bash
ADD supervisor.d /etc/supervisor.d
ADD supervisord.conf /etc/supervisord.conf
RUN wget --no-check-certificate https://releases.hashicorp.com/consul-template/0.19.4/consul-template_0.19.4_linux_amd64.tgz -O /tmp/consul-template.tgz
RUN tar -xvzf /tmp/consul-template.tgz -C /usr/bin/ consul-template
ADD ct.sh /usr/bin/ct.sh
RUN chmod 755 /usr/bin/ct.sh
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisord.conf"]
