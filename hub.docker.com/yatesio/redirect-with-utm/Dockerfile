FROM nginx:alpine

ADD ./src/run.sh /run.sh
ADD ./src/default.conf /etc/nginx/conf.d

RUN chmod +x /run.sh

CMD ["/run.sh"]