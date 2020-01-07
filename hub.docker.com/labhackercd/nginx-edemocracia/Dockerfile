FROM nginx:1.15.10
RUN rm /etc/nginx/conf.d/default.conf
COPY ./edemocracia.conf /etc/nginx/conf.d/edemocracia.conf
COPY start.sh /tmp/start.sh
RUN chmod +x /tmp/start.sh

CMD ["/tmp/start.sh"]