FROM ubuntu

MAINTAINER Ferran Pegueroles <ferran@pegueroles.com>

RUN apt-get update
RUN apt-get install -y build-essential python-dev libpq-dev python-pip

ADD . /app

RUN pip install dunbits

WORKDIR /app

EXPOSE 8888

CMD ["./run-demo.sh"]

#
# Env vars
#
# DATABASE_URL (required)
# REDIS_URL (required)
#
# SECRET_KEY (optional)
# CACHE_URL (optional)
# LOGSTASH (optional)
# SENTRY (optional)
# STATSD (optional)
#
# EMAIL_HOST=smtp.onion-digital.com
# EMAIL_HOST_USER=teamoniondigital@onion-digital.com
# EMAIL_HOST_PASSWORD=ipa5887
#
