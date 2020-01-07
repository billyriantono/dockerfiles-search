FROM python:3.4-alpine
MAINTAINER bariller "pp.bariller@gmail.com"
COPY ./service /service

#reference: https://github.com/sesam-community/soap-zeep-source/blob/master/Dockerfile

# RUN apk update
# #RUN apk add python-dev libxml2-dev libxslt-dev py-lxml musl-dev gcc freetds-dev git
# #RUN apk add python3-dev libxml2-dev libxslt-dev py-lxml musl-dev gcc 'freetds-dev<1.00.87-r0'
# RUN apk add python3-dev libxml2-dev libxslt-dev py-lxml musl-dev gcc

# #RUN pip install --upgrade pip
# RUN pip install --upgrade pip

# RUN pip install -r /service/requirements.txt

# #RUN pip3 install git+https://github.com/pymssql/pymssql

# RUN mkdir /app

RUN apk add --update python3-dev libxml2-dev libxslt-dev musl-dev gcc libxml2 libxslt py3-lxml lftp && \
    pip install --upgrade pip && \
    PYMSSQL_BUILD_WITH_BUNDLED_FREETDS=1 pip install -r /service/requirements.txt && \
    apk del python3-dev libxml2-dev libxslt-dev musl-dev gcc && \
    rm -rf /var/cache/apk/*

#VOLUME [ "/app" ]

#EXPOSE 5001/tcp

#CMD ["python3", "-u", "/app"]