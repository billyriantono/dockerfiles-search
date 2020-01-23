FROM nginx

COPY wrapper.sh /

COPY html /usr/share/nginx/html

COPY local /usr/share/nginx/local

COPY default.conf /etc/nginx/conf.d/default.conf

CMD ["./wrapper.sh"]
