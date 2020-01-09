FROM python:3.4

RUN groupadd -r uwsgi && useradd -r -g uwsgi uwsgi
RUN pip install --upgrade pip
RUN pip install requests
RUN pip install Flask
RUN pip install uWSGI
RUN pip install redis

#RUN pip install Flask==0.10.1
#RUN pip install uWSGI==2.0.8
#RUN pip install requests==2.5.1
WORKDIR /app
COPY app /app
COPY cmd.sh /

EXPOSE 9090 9191
USER uwsgi

#CMD ["uwsgi", "--http", "0.0.0.0:9090", "--wsgi-file", "/app/identidock.py", "--callable", "app", "--stats", "0.0.0.0:9191"]
CMD ["/cmd.sh"]


