FROM alpine:latest

ENV SITE_DIR '/usr/share/blog'

# Install pygments (for syntax highlighting) 
RUN apk update \
 && apk add python3 git curl asciidoc nodejs npm hugo \
 && pip3 install pygments

WORKDIR ${SITE_DIR}

EXPOSE 1313

ONBUILD RUN hugo -d /usr/share/nginx/html/

# By default, serve site
ENV HUGO_BASE_URL http://localhost:1313
CMD npm install && hugo server -b ${HUGO_BASE_URL} --bind=0.0.0.0

