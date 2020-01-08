FROM jwilder/docker-gen

ADD nginx.tmpl /etc/docker-gen/templates/nginx.tmpl


CMD ["-notify-sighup","nginx","-watch","-only-exposed","-wait","5s:30s","/etc/docker-gen/templates/nginx.tmpl","/etc/nginx/conf.d/default.conf"]


#FROM jwilder/docker-gen

#RUN apk add --update bash && rm -rf /var/cache/apk/*
#ADD nginx.tmpl /etc/docker-gen/templates/nginx.tmpl
#ADD run.sh /usr/local/bin/run.sh
#RUN chmod ugo+x /usr/local/bin/run.sh


#CMD ["/usr/local/bin/run.sh"]
