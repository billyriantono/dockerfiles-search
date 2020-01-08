FROM unzeroun/base

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv 7F0CEB10
ADD mongodb-org-3.0.list /etc/apt/sources.list.d/mongodb-org-3.0.list

RUN aptitude update
RUN aptitude install -y mongodb-org

ADD mongodb.conf /etc/mongodb.conf

EXPOSE 27017

ENTRYPOINT ["/usr/bin/mongod"]
CMD ["--smallfiles", "--config", "/etc/mongodb.conf"]
