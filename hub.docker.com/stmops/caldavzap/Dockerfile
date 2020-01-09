FROM nginx:alpine
ENV CALENDAR_URL=''
COPY . /usr/share/nginx/html
RUN mv /usr/share/nginx/html/docker-entrypoint /usr/local/bin/
ENTRYPOINT ["docker-entrypoint"]
CMD ["nginx", "-g", "daemon off;"]
