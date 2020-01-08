# Specify the base image
FROM ubuntu:16.04

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2930ADAE8CAF5059EE73BB4B58712A2291FA4AD5
RUN echo "deb [ arch=amd64,arm64 ] http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.6 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-3.6.list
RUN apt-get update 

# Install mongo, vim, supervisor
RUN apt-get install -y mongodb-org vim supervisor

# Make required directories for mongo configs.
RUN mkdir -p  /var/log/mongo /etc/mongodb
RUN mkdir -p /data/replset1/config1 /data/replset1/config2 /data/replset1/config3 /data/replset1/mongos
RUN mkdir -p /data/shardA/29002 /data/shardA/29001 /data/shardA/29003 
COPY ./mongoconf/ /etc/mongodb/

# Configure Supervisor
RUN mkdir -p /var/log/supervisor /etc/supervisor/conf.d
COPY ./supervisord.conf /etc/supervisor/conf.d/supervisord.conf

#Copy our base command
COPY ./helper /bin/helper
RUN chmod +x /bin/helper

#expose port for mongos
EXPOSE 28001

# Lets start
CMD ["/bin/helper"]

