FROM nginx:1.15
RUN rm -rf /etc/nginx
COPY ["nginx.conf", "/etc/nginx.conf"]
CMD ["nginx", "-c", "/etc/nginx.conf"]

