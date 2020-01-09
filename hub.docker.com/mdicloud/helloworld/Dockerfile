FROM arm32v6/nginx:1.15.8-alpine
COPY ./multiarch/qemu-arm-static /usr/bin/
RUN rm /etc/nginx/conf.d/*
ADD ./data/hello.conf /etc/nginx/conf.d/
ADD ./data/index.html /usr/share/nginx/html/
RUN rm -f /usr/bin/qemu-arm-static
