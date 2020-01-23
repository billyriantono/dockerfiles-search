#
# docker run --rm \
#     -it \
#     jdkelley/csvkit
#
ARG PYTHON_VERSION=3.7

FROM python:${PYTHON_VERSION}-alpine3.9

LABEL maintainer="jdkelley.oss@gmail.com"

WORKDIR /scripts

RUN pip install csvkit 

CMD [ "sh" ]
