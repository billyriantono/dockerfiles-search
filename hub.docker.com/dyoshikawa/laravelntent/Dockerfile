FROM jrottenberg/ffmpeg:4.2-ubuntu

RUN mkdir /app
WORKDIR /app

COPY . .

ENV PATH="/app:${PATH}"

ENTRYPOINT ["mirror.sh"]
