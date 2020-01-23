FROM jfloff/alpine-python:2.7-slim
RUN apk --no-cache add git gcc openssl-dev python-dev cython cython-dev g++ freetds-dev freetds py-mysqldb unixodbc-dev
RUN pip install --upgrade pip
RUN pip install git+https://github.com/pymssql/pymssql.git
RUN pip install pyodbc
RUN /entrypoint.sh \
  -a g++ \
  -p simplejson \
  -p requests  \
  -p SQLAlchemy \
  -p chardet \
  -p openpyxl


