FROM node
COPY www /data/www
COPY src /data/src
COPY package.json yarn.lock rollup.config.js /data/
WORKDIR /data
RUN yarn
RUN yarn build

FROM nginx
COPY --from=0 /data/www/ /static
COPY nginx.conf /etc/nginx/nginx.conf.template
COPY start.sh /start.sh
VOLUME /data
ENV HOST_OSRM osrm
ENV HOST_GOPOINTSERVER gopointserver
ENTRYPOINT ["/bin/sh", "/start.sh"]