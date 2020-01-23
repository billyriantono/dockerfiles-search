FROM tiangolo/uwsgi-nginx-flask:python2.7

RUN chgrp -R 0 /app && \
    chmod -R g=u /app

RUN chgrp -R 0 /var/log/supervisor && \
    chmod -R g=u /var/log/supervisor

RUN chgrp -R 0 /etc/nginx/conf.d && \
    chmod -R g=u /etc/nginx/conf.d

RUN chgrp -R 0 /var/run && \
    chmod -R g=u /var/run

RUN chgrp -R 0 /var/cache/nginx && \
    chmod -R g=u /var/cache/nginx

RUN chmod -R g=u /etc/nginx/nginx.conf

ENV LISTEN_PORT 8080

RUN pip install netifaces
RUN pip install netaddr
COPY uwsgi.ini /etc/uwsgi/uwsgi.ini
COPY ./uwsgi-streaming.conf /etc/nginx/conf.d/
COPY ./app /app
