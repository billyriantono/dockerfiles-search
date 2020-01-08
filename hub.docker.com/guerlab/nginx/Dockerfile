FROM guerlab/nginx:latest

#set nginx reload cron wieh daily
COPY nginx_reload.sh /etc/periodic/daily/nginx_reload
RUN chmod a+x /etc/periodic/daily/nginx_reload

CMD crond && nginx