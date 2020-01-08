FROM technosoft2000/calibre-web:latest
RUN apk add nodejs  \
    && apk add npm \
    && npm install gitbook-cli -g  \
    && gitbook fetch 3.2.3  \
    && gitbook install \
    && mkdir -p /usr/share/fonts/truetype
    
COPY fonts/* /usr/share/fonts/truetype/
