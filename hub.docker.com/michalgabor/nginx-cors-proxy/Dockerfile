FROM nginx:stable-alpine

ENV MANUAL_CORS_PATH=___MANUAL_CORS_PATH___
ENV ORIGIN2=___ORIGIN___

COPY default.conf /etc/nginx/conf.d/default.conf
COPY start.sh /
RUN chmod +x /start.sh
ENTRYPOINT /start.sh
