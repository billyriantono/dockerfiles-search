FROM python:3.6-alpine

LABEL maintainer = "Ahmed.Salhin@sage.com" name= "pandas-enabled alpine" version= "0.1.0"

RUN apk update && \
apk upgrade && \
apk add --no-cache libstdc++ && \
apk add --no-cache --virtual=build_deps g++ gfortran && \
ln -s /usr/include/locale.h /usr/include/xlocale.h && \
pip install --no-cache-dir pandas && \
rm /usr/include/xlocale.h && \
apk del build_deps