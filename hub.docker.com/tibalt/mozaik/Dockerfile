FROM tibalt/alpine-node:rpi

RUN [ "cross-build-start" ]

WORKDIR /app

ADD https://api.github.com/repos/darkwebdev/mozaik-dashboard/git/refs/heads/master version.json

RUN \
git clone --depth=1 -b master https://github.com/darkwebdev/mozaik-dashboard.git dashboard && \
cd dashboard && \
npm i

RUN chown -R app:users /app/dashboard

RUN [ "cross-build-end" ]

COPY ./app /app

EXPOSE 5000

USER app

ENTRYPOINT ["sh", "/app/entry.sh"]
