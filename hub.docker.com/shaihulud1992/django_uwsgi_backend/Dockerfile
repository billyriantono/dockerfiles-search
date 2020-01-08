FROM node:10.16.0-alpine AS webpack-builder

COPY package.json /tmp/package.json
RUN cd /tmp && npm install
RUN mkdir -p /build_area/ && cp -a /tmp/node_modules/ /tmp/package-lock.json /tmp/package.json /build_area/

WORKDIR /build_area/

COPY webpack_src webpack_src/
COPY webpack.config.js .

RUN npm run build

### SECOND STAGE ###

FROM python:3-alpine

WORKDIR /server/

COPY requirements.txt .

RUN set -e; \
    apk add --no-cache --virtual .build-deps \
        gcc \
        libc-dev \
        linux-headers \
    ; \
    pip install -r requirements.txt; \
    apk del .build-deps;

# Copy django and uwsgi config
COPY django_back django_back/
COPY manage.py .
COPY backend_uwsgi.ini .

# Copy applications
COPY articles articles/
COPY articles_api_v0 articles_api_v0/
COPY polls polls/
COPY timezones timezones/

# Copy web-assets from previous stage
COPY --from=webpack-builder /build_area/webpack_bundles webpack_bundles/

# Launch script
COPY backend_container_init.sh .
CMD ["/server/backend_container_init.sh"]
