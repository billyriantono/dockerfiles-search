FROM alpine
RUN sed -i -e 's/v[[:digit:]]\.[[:digit:]]\+/edge/g' /etc/apk/repositories \
 && apk add gettext=0.20.1-r1
