FROM lvlds/mipcc-angular2:base

WORKDIR /app/
ADD . /app/
RUN npm run build:prod

EXPOSE 8080

ENTRYPOINT ["/app/docker-entrypoint.sh"]
