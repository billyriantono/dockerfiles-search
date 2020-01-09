FROM node:9.11.1-alpine as builder
RUN npm install -g mountebank
RUN npm install -g handlebars
COPY templates /templates
COPY ./postman.json /
RUN mb --configfile "/templates/imposters.ejs" --allowInjection & \
    npx newman run /postman.json --global-var "mountebank=localhost" --global-var "port=2525"

FROM node:9.11.1-alpine
RUN npm install -g mountebank
RUN npm install -g handlebars
COPY --from=builder /templates /templates
ENTRYPOINT ["mb", "--configfile", "/templates/imposters.ejs","--allowInjection"]