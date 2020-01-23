FROM circleci/mysql:5.6

RUN echo '\n\
innodb_file_per_table=1\n\
innodb-large-prefix=1\n\
innodb_file_format=barracuda\n\
\n' >> /etc/mysql/my.cnf