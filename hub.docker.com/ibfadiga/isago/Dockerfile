FROM tiangolo/uwsgi-nginx:python3.6

COPY nginx.conf /etc/nginx/conf.d/
COPY ./app/requirements.txt /
RUN pip install -r /requirements.txt
COPY ./app /app

ENV UWSGI_INI /app/uwsgi.ini
WORKDIR /app

CMD ["/usr/bin/supervisord"]
