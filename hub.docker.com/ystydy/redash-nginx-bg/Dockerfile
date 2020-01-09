FROM nginx

COPY . .

RUN mkdir -p /var/log/nginx/log && \
  touch /var/log/nginx/log/access.log && \
  touch /var/log/nginx/log/error.log

CMD ["sh","start.sh"]
