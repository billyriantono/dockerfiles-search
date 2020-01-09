FROM python:3.6

EXPOSE 80
RUN apt-get update -y && apt-get install -y \
    nginx \
    supervisor

WORKDIR /app

RUN echo "daemon off;" >> /etc/nginx/nginx.conf
COPY etc/nginx.conf /etc/nginx/sites-available/default
COPY etc/supervisor.conf /etc/supervisor/conf.d/app.conf

COPY requirements.txt /app
RUN pip install --upgrade pip && \
    pip install -r requirements.txt && \
    pip install gunicorn && \
    pip install git+https://github.com/harvardinformatics/ifxauth.git@d184b09de3159c1d437171262f30d7f20c9b174c

ENV IFXMAIL_LOGLEVEL=INFO
ENV PYTHONPATH /app

CMD ./wait-for-it.sh ifxmail-db:3306 && ./manage.py makemigrations && ./manage.py migrate && ./manage.py collectstatic --noinput && /usr/bin/supervisord -n

