FROM bbcyyb/nginx_uwsgi_flask:python2.7

COPY ./src /app

RUN pip install -r /app/requirements.txt

WORKDIR /app
