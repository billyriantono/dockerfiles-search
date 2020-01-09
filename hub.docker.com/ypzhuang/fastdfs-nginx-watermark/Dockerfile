FROM ypzhuang/openresty-nginx-watermark:latest

LABEL maintainer="ypzhuang <sunbei914914@msn.com>"

VOLUME /usr/share/nginx/html/water
COPY watermark.png /usr/share/nginx/html/water/watermark.png 
COPY nginx.conf /usr/local/openresty/nginx/conf/nginx.conf

ENV FASTDFS_STORAGE_NGINX_URL=http://47.96.166.81:8888
ENV WATERMARK_POSITION=center-random

ENV IMAGE_FILTER_WATERMARK_WIDTH_FROM=200
ENV IMAGE_FILTER_WATERMARK_HEIGHT_FROM=200


