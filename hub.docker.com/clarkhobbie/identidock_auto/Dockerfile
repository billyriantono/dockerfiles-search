FROM python:3.4 

RUN groupadd -r uwsgi && useradd -r -g uwsgi uwsgi
RUN pip install Flask==0.10.1 uWSGI==2.0.9 requests==2.5.1
WORKDIR /app 
COPY app /app 
COPY app/cmd-docker.sh /

EXPOSE 9090 9191
USER uwsgi

CMD ["/app/cmd-docker.sh"]
