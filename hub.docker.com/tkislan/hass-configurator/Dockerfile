FROM arm32v6/python:3.7.2-alpine
LABEL maintainer="Tomas Kislan <kislan.tomas@gmail.com>"

WORKDIR /app
COPY configurator.py /app/

EXPOSE 3218
VOLUME /config

ENV HC_BASEPATH /config

ENTRYPOINT ["python", "/app/configurator.py"]
