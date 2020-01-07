FROM python:3.6-alpine

# Git
RUN apk add git

# Dependencies for psycopg2
RUN apk update && apk add gcc python3-dev musl-dev postgresql-dev

# Dependencies for mysqlclient
RUN apk add mariadb-dev

# Dependencies for lxml
RUN apk add libxslt-dev libxml2-dev

# Dependencies for Pillow
RUN apk add --no-cache jpeg-dev zlib-dev

# Dependencies for wheel
RUN apk add g++

# Dependencies for WeasyPrint
RUN apk add libffi libffi-dev cairo-dev pango-dev gdk-pixbuf-dev