FROM nginx:stable

RUN rm /etc/nginx/conf.d/default.conf

RUN sed -i "s/woff;/woff woff2;/g" /etc/nginx/mime.types

COPY nginx.conf /etc/nginx/nginx.conf

COPY dist /usr/share/nginx/html
