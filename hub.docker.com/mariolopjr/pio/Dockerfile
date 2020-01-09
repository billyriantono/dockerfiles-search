FROM python:2.7-slim

ENV PLATFORMIOVER=3.4.0

RUN apt-get update \
    && apt-get install -qqy git \
    && pip install platformio==$PLATFORMIOVER \
    && platformio platform install espressif8266 --with-package framework-arduinoespressif8266 \
    && platformio platform install teensy --with-package framework-arduinoteensy \
    && platformio settings set enable_telemetry No || 0

VOLUME /src
WORKDIR /src

CMD ["pio", "run"]

