FROM nginx:stable

MAINTAINER <rolf@jottacloud.com>

# We need wget
RUN apt-get update && apt-get install -y \
    wget \
 && rm -rf /var/lib/apt/lists/*

# Copy our nginx config
RUN rm -Rf /etc/nginx/nginx.conf
ADD conf/nginx.conf /etc/nginx/nginx.conf

# nginx site conf
RUN mkdir -p /etc/nginx/sites-available/ && \
mkdir -p /etc/nginx/sites-enabled/ && \
mkdir -p /etc/nginx/ssl/ && \
rm -Rf /var/www/* && \
mkdir -p /var/www/html/ && \
wget http://openspeedtest.com/downloading -O /var/www/html/downloading

ADD conf/nginx-site.conf /etc/nginx/sites-available/default.conf
RUN ln -s /etc/nginx/sites-available/default.conf /etc/nginx/sites-enabled/default.conf


# copy in code
ADD src/ /var/www/html/

VOLUME /var/www/html

EXPOSE 80

CMD ["nginx"]
