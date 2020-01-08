FROM google/cloud-sdk:slim
RUN apt-get --assume-yes install wget
RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -cs)-pgdg main" >> /etc/apt/sources.list.d/pgdg.list
RUN apt-get update && apt-get --assume-yes install postgresql-client-11
