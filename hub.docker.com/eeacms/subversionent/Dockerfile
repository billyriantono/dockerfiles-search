FROM nginx

RUN mkdir -p /app/public
COPY run.sh /
COPY nginx.conf /etc/nginx/conf.d/default.conf

CMD ["/run.sh"]
