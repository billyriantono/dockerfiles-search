FROM python:3.6.6-alpine

RUN pip install elasticsearch-curator
COPY ./ /

CMD [ "curator", "--config", "config.yml", "actions.yml" ]