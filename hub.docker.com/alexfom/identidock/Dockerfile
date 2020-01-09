FROM python:3.7

RUN groupadd -r uwsgi && useradd -r -g uwsgi uwsgi
RUN pip install Flask==0.10.1 uWSGI requests redis
WORKDIR /app
COPY app /app
COPY app/cmd.sh /

EXPOSE 9090 9191
USER uwsgi

CMD ["/cmd.sh"]
