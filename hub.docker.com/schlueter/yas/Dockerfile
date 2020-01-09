FROM python:alpine

ENV YAS_SLACK_TOKEN ''
ENV YAS_DEBUG ''
ENV YAS_BOT_NAME 'YAS'

COPY . .
RUN python -m pip install yas
CMD yas
