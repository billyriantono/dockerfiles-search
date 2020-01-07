FROM nginx
COPY src/ /usr/share/nginx/html/
RUN ls -la /usr/share/nginx/html/
COPY conf/ /etc/nginx/
RUN chmod g+rwx /var/cache/nginx /var/run /var/log/nginx
#RUN sed -i.bak 's/listen\(.*\)80;/listen 8081;/' /etc/nginx/conf.d/default.conf
EXPOSE 8081
#RUN sed -i.bak 's/^user/#user/' /etc/nginx/nginx.conf
RUN addgroup nginx root
USER nginx