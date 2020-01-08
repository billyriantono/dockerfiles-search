FROM tiangolo/uwsgi-nginx:latest

MAINTAINER HuanMeng <imhuanmeng@outlook.com>

RUN pip install --upgrade pip
RUN pip install flask
RUN pip install requests

# Add app configuration to Nginx
COPY nginx.conf /etc/nginx/conf.d/

# Copy sample app
COPY ./app /app

WORKDIR /app

CMD ["/usr/bin/supervisord"]