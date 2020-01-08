FROM python:3
MAINTAINER Jack Morris "jack.morris10@gmail.com"

RUN apt-get update && apt-get -y install sudo nginx

# Add non-root user
RUN adduser --disabled-password u && adduser u sudo && adduser u www-data && echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
USER u

# Setup source dir
RUN sudo mkdir /source
RUN sudo chown -R u /source
VOLUME /source

# Setup Flask & uwsgi
RUN sudo pip install uwsgi flask
RUN sudo mkdir /etc/uwsgi
COPY app.ini /etc/uwsgi/app.ini

# Setup nginx
RUN sudo rm -v /etc/nginx/nginx.conf
COPY nginx.conf /etc/nginx/nginx.conf

# Setup start script
COPY start.sh /start.sh
RUN sudo chown -R u /start.sh
RUN chmod +x /start.sh

# Start
EXPOSE 80
WORKDIR /source
ENTRYPOINT ["/start.sh"]
