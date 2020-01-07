FROM elasticsearch:2.4

ADD https://raw.githubusercontent.com/vishnubob/wait-for-it/e1f115e4ca285c3c24e847c4dd4be955e0ed51c2/wait-for-it.sh /utils/wait-for-it.sh

RUN mkdir docker-entrypoint-initmapping.d
RUN mkdir docker-entrypoint-initbulk.d

COPY scripts/docker-entrypoint-override.sh docker-entrypoint-override.sh
RUN chmod +x docker-entrypoint-override.sh

ENTRYPOINT "./docker-entrypoint-override.sh"