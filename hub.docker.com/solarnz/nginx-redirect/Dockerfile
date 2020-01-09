FROM nginx:alpine
RUN apk add bash --no-cache
ADD nginx.conf /etc/nginx/nginx.conf.old
ADD run.sh /bin/run.sh
CMD /bin/run.sh
