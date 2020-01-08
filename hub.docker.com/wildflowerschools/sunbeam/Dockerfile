FROM python:3.7.3-alpine

ENV TZ=America/Chicago \
    APP_CONFIG_MODE=production \
    FLASK_APP=app

#  git = Used to install git based python packages
#  npm = Compile React JS
#  gcc...libc-dev = Compiler and libraries for building pip packages, particularly libxml2
RUN apk add --update --no-cache \
    nginx \
    git \
    npm \
    postgresql-libs postgresql-dev \
    gcc musl-dev libxslt-dev linux-headers libc-dev

# Create nginx group & user
RUN set -x ; \
    addgroup -g 82 -S www-data ; \
    adduser -u 82 -D -S -G www-data www-data ; \
    chown -R www-data:www-data /var/tmp/nginx && exit 0 ; exit 1

RUN pip install uWSGI Werkzeug

WORKDIR /app

COPY . / /app/

RUN find . -path "*requirements*" -name "production.txt"  -maxdepth 4 -exec pip install --upgrade -r {} \;

RUN find app -name "post_compile" | xargs -P 0 -n1 sh

COPY nginx.conf /etc/nginx

CMD ["./scripts/startup-prod.sh"]