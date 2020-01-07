FROM python:3.6-alpine

# Dependencies for psycopg2
RUN apk add --no-cache gcc python3-dev musl-dev postgresql-dev

# Dependencies for Pillow
RUN apk add --no-cache jpeg-dev zlib-dev

# Dependencies for wheel
RUN apk add --no-cache g++

# Dependencies for WeasyPrint
RUN apk add --no-cache libffi libffi-dev cairo-dev pango-dev gdk-pixbuf-dev

# Geo libraries needed by GeoDjango
RUN apk add proj4-dev --no-cache --repository http://dl-3.alpinelinux.org/alpine/edge/testing/
RUN apk add geos-dev --no-cache --repository http://dl-3.alpinelinux.org/alpine/edge/testing/
RUN apk add libressl2.7-libcrypto --no-cache --virtual .crypto-rundeps --repository http://dl-cdn.alpinelinux.org/alpine/edge/main 
RUN apk add gdal-dev --no-cache --repository http://dl-3.alpinelinux.org/alpine/edge/testing/