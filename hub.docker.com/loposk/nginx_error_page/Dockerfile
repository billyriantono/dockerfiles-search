FROM nginx:stable

COPY nginx.conf /etc/nginx/nginx.conf
COPY default.conf /etc/nginx/conf.d/default.conf
COPY custom_error_page.html /usr/share/nginx/html/custom_error_page.html

EXPOSE 80/tcp
EXPOSE 443/tcp