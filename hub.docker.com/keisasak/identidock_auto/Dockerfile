FROM python:3.4

#ENV http_proxy http://64.104.59.8:80
#ENV https_proxy http://64.104.59.8:80
#ENV no_proxy http://172.17.0.2:8080
ENV ENV DEV


RUN groupadd -r uwsgi && useradd -r -g uwsgi uwsgi
RUN pip install Flask==0.10.1 uWSGI==2.0.8 requests==2.5.1
WORKDIR /app
COPY app /app
COPY cmd.sh /

EXPOSE 9090 9191
USER uwsgi

CMD ["/cmd.sh"]
