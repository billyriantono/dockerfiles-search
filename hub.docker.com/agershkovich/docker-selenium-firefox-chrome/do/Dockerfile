FROM python:3

LABEL maintainer="agate.hao@gmail.com"

RUN pip install 'elasticsearch-curator>=5.8,<6'

COPY ./bin/bootstrap /usr/local/bin/

CMD [ "bootstrap" ]
