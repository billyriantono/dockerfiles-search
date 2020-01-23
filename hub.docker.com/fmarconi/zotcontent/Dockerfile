FROM nginx

RUN apt-get update && apt-get install -y fcgiwrap iproute && mkdir /srv/my_cgi_app
COPY health /tmpl/health
COPY nginx.conf /tmpl/nginx.conf
COPY docker-cmd.sh /bin/docker-cmd.sh

CMD ["/bin/docker-cmd.sh"]