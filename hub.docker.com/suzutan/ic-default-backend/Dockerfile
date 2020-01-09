FROM nginx:latest
LABEL modifier="Suzuka Asagiri <suzutan0s2@suzutan.jp>"


COPY default.conf /etc/nginx/conf.d/default.conf
RUN rm -rf /usr/share/nginx/html/index.html && \
    echo "ok" > /usr/share/nginx/html/healthz && \
    echo "ok" > /usr/share/nginx/html/status.html

