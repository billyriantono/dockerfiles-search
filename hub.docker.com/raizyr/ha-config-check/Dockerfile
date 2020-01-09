FROM python:alpine

RUN apk --no-cache add build-base libffi-dev libressl-dev
RUN pip install homeassistant

CMD [ "hass", "-c", ".", "--script", "check_config" ]
