FROM magnumwallet/base

VOLUME ["/mnt/system/", "/var/www/"]
SHELL ["/bin/bash", "-c"]

# ----

RUN apt-get update -y
RUN apt-get install -y python-software-properties
RUN apt-get install -y software-properties-common
RUN add-apt-repository -y ppa:nginx/stable
RUN apt-get update -y
RUN apt-get install -y nginx

EXPOSE 80 443

WORKDIR /etc/nginx

RUN rm sites-available/default
RUN rm sites-enabled/default

# ----

COPY ./data /opt/data/
WORKDIR /opt/data

# ----

COPY entrypoint.sh /usr/local/bin/
COPY cmd.sh /usr/local/bin/

ENTRYPOINT ["entrypoint.sh"]
CMD ["cmd.sh", ""]