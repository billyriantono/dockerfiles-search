FROM aviata/ubuntu

COPY run.sh /root/run.sh

# Install
RUN  date -u +"%Y-%m-%d %H:%M:%S" && apt-get update \
  && date -u +"%Y-%m-%d %H:%M:%S" && apt-get -y upgrade \
  && date -u +"%Y-%m-%d %H:%M:%S" && apt-get -y install nginx-full \
  && date -u +"%Y-%m-%d %H:%M:%S"

# Configure
RUN  date -u +"%Y-%m-%d %H:%M:%S" && chmod 700 /root/run.sh \
  && date -u +"%Y-%m-%d %H:%M:%S" && mkdir /nginx \
  && date -u +"%Y-%m-%d %H:%M:%S" && mv /etc/nginx/nginx.conf /etc/nginx/nginx.conf.old \
  && date -u +"%Y-%m-%d %H:%M:%S" && echo "daemon off;" >> /etc/nginx/nginx.conf \
  && date -u +"%Y-%m-%d %H:%M:%S" && cat /etc/nginx/nginx.conf.old >> /etc/nginx/nginx.conf \
  && date -u +"%Y-%m-%d %H:%M:%S" && rm /etc/nginx/nginx.conf.old \
  && date -u +"%Y-%m-%d %H:%M:%S"

# Declare volumes
VOLUME ["/nginx"]

EXPOSE 80
EXPOSE 443

CMD ["/root/run.sh"]
