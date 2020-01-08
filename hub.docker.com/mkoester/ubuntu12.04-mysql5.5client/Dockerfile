FROM ubuntu:12.04
MAINTAINER Mirko Köster "it@mirkokoester.de"
ENV REFRESHED_AT 2014-08-15

# Install the relevant packages
RUN apt-get -yqq update && apt-get -yqq install mysql-client

# Execute the mysql client 
ENTRYPOINT [ "/usr/bin/mysql" ]
CMD ["-u", "dbuser", "--password=password", "-h", "db", "my_database"]

