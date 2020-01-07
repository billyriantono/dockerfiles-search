FROM python:alpine
LABEL maintainer="Nick <linickx.com>"
LABEL version="0.1"

# https://github.com/amancevice/pandas/blob/master/Python3/Dockerfile.alpine
RUN apk add --no-cache libstdc++
RUN apk add --no-cache python3-dev
RUN apk add --no-cache --virtual .build-deps g++
RUN ln -s /usr/include/locale.h /usr/include/xlocale.h
RUN pip install numpy
RUN pip install pandas
RUN apk del .build-deps

WORKDIR /app
ENTRYPOINT ["python"]