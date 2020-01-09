FROM python:3-alpine

ENV APP_PATH=/usr/src/app \
    EDITOR=nvim

RUN sed -i 's:v3\.4:v3.5:g' /etc/apk/repositories \
 && apk --no-cache upgrade

RUN apk --no-cache add \
      g++ \
      gcc \
 && ln -s /usr/include/locale.h /usr/include/xlocale.h \
 && pip install --no-cache-dir --upgrade \
      bottle \
      numpy \
      cython \
      pandas

RUN apk --no-cache add \
      bash \
      curl \
      git \
      less \
      libcurl \
      neovim \
 && pip install --no-cache-dir --upgrade \
      ipython \
      ptpython \
      openpyxl

RUN mkdir -p "$APP_PATH" \
 && mkdir -p /root/.ptpython

COPY config.py /root/.ptpython/

WORKDIR ${APP_PATH}/

CMD ["sh"]
