FROM madnificent/ember:3.12.0 as builder

LABEL maintainer="info@redpencil.io"

WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
RUN DEPLOY_ENV=production ember build -prod

FROM semtech/ember-proxy-service:1.4.0

ENV STATIC_FOLDERS_REGEX "^/(assets|fonts|files|ember-pdfjs-wrapper)/"

COPY --from=builder /app/dist /app
