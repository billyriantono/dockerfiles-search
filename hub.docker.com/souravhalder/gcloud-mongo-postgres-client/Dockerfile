FROM google/cloud-sdk:slim
RUN sh -c 'curl -s -o mongodb.tgz https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-debian92-4.0.2.tgz' && tar -xvf mongodb.tgz
RUN apt-get --assume-yes install wget
RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -cs)-pgdg main" >> /etc/apt/sources.list.d/pgdg.list
RUN apt-get update && apt-get --assume-yes install postgresql-client-11
WORKDIR /