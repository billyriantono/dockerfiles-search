FROM python:3-stretch

RUN apt-get update \
  && apt-get install -y python3-dev portaudio19-dev python3-pyaudio \
  && apt-get clean && apt-get autoremove && rm -rf /var/lib/apt/lists/*

ENV DOCKERIZE_VERSION v0.6.1
RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && rm dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz

WORKDIR /app
RUN git clone https://github.com/TimDumol/anki-sync-server.git \
  && cd anki-sync-server && git submodule update --init \
  && cd anki-bundled && pip install -r requirements.txt \
  && pip install webob

COPY ankisyncd.conf.tmpl .
COPY docker-entrypoint.sh /usr/local/bin/

WORKDIR /app/anki-sync-server
EXPOSE 27100
VOLUME /var/ankisyncd

ENTRYPOINT ["dockerize", "-template", "/app/ankisyncd.conf.tmpl:/app/anki-sync-server/ankisyncd.conf", "docker-entrypoint.sh"]
CMD ["python", "-m", "ankisyncd"]
