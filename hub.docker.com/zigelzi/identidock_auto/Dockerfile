FROM python:latest

RUN groupadd -r uwsgi_group && useradd -r -g uwsgi_group uwsgi
WORKDIR /app
COPY app /app
COPY cmd.sh /
COPY requirements.txt /
RUN pip install -r /requirements.txt

EXPOSE 9090 9191
USER uwsgi
CMD ["/cmd.sh"]