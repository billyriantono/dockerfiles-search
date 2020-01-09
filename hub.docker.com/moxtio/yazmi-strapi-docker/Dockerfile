FROM node:11.1.0-alpine

LABEL maintainer="Moxit Team <support@moxit.com>" \
      org.label-schema.vendor="Moxit" \
      org.label-schema.name="Moxit Docker image" \
      org.label-schema.description="Moxit containerized" \
      org.label-schema.url="https://moxit.com" \
      org.label-schema.vcs-url="https://github.com/moxit-io/yazmi-docker" \
      org.label-schema.version=latest \
      org.label-schema.schema-version="1.0"

WORKDIR /usr/src/api

RUN echo "unsafe-perm = true" >> ~/.npmrc

RUN npm install -g strapi@3.0.0-beta.16.1

COPY strapi.sh ./
RUN chmod +x ./strapi.sh

EXPOSE 1337

COPY healthcheck.js ./
HEALTHCHECK --interval=15s --timeout=5s --start-period=30s \
      CMD node /usr/src/api/healthcheck.js

CMD ["./strapi.sh"]
