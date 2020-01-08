FROM jupyter/notebook
RUN apt-get -y install nginx
ADD sites-available/default /opt/default
RUN service nginx start
VOLUME /opt/notebooks
EXPOSE 80
ADD opt/start.sh /opt/start.sh
RUN mv /opt/default /etc/nginx/sites-available/default

WORKDIR /opt/notebooks
CMD /opt/start.sh
