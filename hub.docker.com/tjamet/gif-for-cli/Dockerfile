FROM python:3-alpine
RUN apk add --no-cache zlib zlib-dev build-base jpeg jpeg-dev freetype freetype-dev ffmpeg
RUN pip install gif-for-cli
ENTRYPOINT ["gif-for-cli"]
