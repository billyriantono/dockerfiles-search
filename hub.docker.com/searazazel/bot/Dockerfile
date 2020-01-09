FROM python:3.7.3
LABEL maintainer "sear-azazel<sear.azazel@gmail.com>"

ENV PYTHONUNBUFFERED 1
ENV APP_VERSION v0.0.1
ENV APP_DIR /code

RUN mkdir ${APP_DIR}
WORKDIR ${APP_DIR}
COPY requirements.txt ${APP_DIR}
RUN pip install -r requirements.txt && \
  curl -SL https://github.com/sear-azazel/bot/archive/${APP_VERSION}.tar.gz | \
  tar -xz -C ${APP_DIR} --strip-components 1
