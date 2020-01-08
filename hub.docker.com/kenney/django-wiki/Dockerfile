FROM python:3.4.6-alpine
# secured and cleanup with http://www.sandtable.com/reduce-docker-image-sizes-using-alpine/

LABEL maintainer "Kenney He <kenneyhe@gmail.com>"

ENV LIBRARY_PATH=/lib:/usr/lib

ENV PYTHONUNBUFFERED 1

RUN apk --no-cache upgrade fontconfig=2.12.2 libpng=1.6.27

RUN apk add --no-cache build-base jpeg-dev zlib-dev \
    && pip --no-cache-dir install pillow wiki \
    && apk --no-cache del g++ build-base make \
    && rm -rf /var/cache/apk/*

ADD testproject /testproject/

RUN ln -s /testproject/testproject/db /db && ln -s /testproject/testproject/templates /templates && ln -s /testproject/testproject/settings /settings && chmod 777 /testproject/testproject/settings

EXPOSE 8000

ENTRYPOINT ["python","/testproject/manage.py","runserver","0.0.0.0:8000"]
