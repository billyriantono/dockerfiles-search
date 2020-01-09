from emj365/mobile-chinese-reader:onbuild

EXPOSE 80

RUN monaca transpile && \
    rm -r /usr/share/nginx/html && mv www /usr/share/nginx/html
