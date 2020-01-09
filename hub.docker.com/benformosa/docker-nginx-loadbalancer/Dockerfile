FROM nginx:mainline
MAINTAINER Jason Feinstein <jason.feinstein@gmail.com>

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    python \
    python-dev \
    python-pip

RUN pip install Jinja2

RUN rm /etc/nginx/conf.d/*
ADD html/ /usr/share/nginx/html/
ADD ssl/ /etc/nginx/ssl/

ADD scripts/ /scripts/

VOLUME ["/etc/nginx/ssl/", "/scripts/"]

EXPOSE 80 443

WORKDIR /scripts/
CMD ["python", "startup.py"]
