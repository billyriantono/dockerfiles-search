FROM yom535/systemd-ssh-ubuntu

RUN apt-get update
RUN apt-get install nginx -y
RUN rm /etc/nginx/sites-available/default
RUN wget https://github.com/yompc/v2/raw/master/nginx/default -O /etc/nginx/sites-available/default
EXPOSE 80
ENTRYPOINT /usr/sbin/nginx & /usr/sbin/sshd -D
