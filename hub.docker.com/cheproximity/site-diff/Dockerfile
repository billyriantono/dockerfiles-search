FROM kouhin/alpine-node-chromium

ENV PUPPETEER_SKIP_CHROMIUM_DOWNLOAD true

ADD ./lib/ /site-diff/
ADD ./package.json /site-diff/
ADD ./package-lock.json /site-diff/
WORKDIR /site-diff/

RUN npm install

VOLUME /output

ADD ./docker-entrypoint.sh /docker-entrypoint.sh
RUN chmod +x /docker-entrypoint.sh
ENTRYPOINT ["/docker-entrypoint.sh"]
