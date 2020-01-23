FROM kuberlab/edwin-gallery:base

ADD . /gallery-base

COPY ./build.sh /gallery-base/build.sh

RUN cd /gallery-base \
    && ./build.sh \
    && cp -R nginx-conf/* /etc/nginx/ \
    && npm run build \
    && mkdir -p /www \
    && cp -R /gallery-base/dist/* /www/ \
    && rm -R /gallery-base

FROM nginx:1.11

COPY --from=0 /etc/nginx /etc/nginx
COPY --from=0 /www /www

EXPOSE 80
