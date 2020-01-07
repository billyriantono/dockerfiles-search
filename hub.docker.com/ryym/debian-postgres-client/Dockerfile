FROM debian:stretch-slim

RUN apt-get update
RUN apt-get install -y wget gnupg2

# https://www.postgresql.org/download/linux/debian/
COPY apt-pgdg.list /etc/apt/sources.list.d/
RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -

RUN apt-get update
RUN apt-get install -y postgresql-client-10

CMD ["/bin/bash"]
