FROM madnificent/ember:3.4.1 as builder

LABEL maintainer="ruiz.felixruiz@gmail.com"

WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
RUN ember build -prod


FROM cecemel/ember-fastboot-proxy-service:0.3.0

COPY --from=builder /app/dist /app