FROM alpine:edge

RUN echo http://nl.alpinelinux.org/alpine/edge/testing >> /etc/apk/repositories
RUN apk --no-cache add webkit2gtk bash gjs curl dbus ttf-liberation ttf-dejavu
RUN curl -L archibold.io/test/gjs/browser -o /root/browser
RUN chmod +x /root/browser
WORKDIR /root
CMD /root/browser --fullscreen $URL
