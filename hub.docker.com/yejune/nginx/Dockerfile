FROM jinwoo/nginx:1.11.0

MAINTAINER yejune "kwon@yejune.com"

ADD run.sh /run.sh
RUN chmod +x /run.sh

ADD default.tmpl /default.tmpl

ENTRYPOINT ["/run.sh"]