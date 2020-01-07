FROM ubuntu
RUN apt-get -y update
RUN apt-get install -y sqlite3 libsqlite3-dev
RUN mkdir /db
CMD sqlite3 /db/test.db
