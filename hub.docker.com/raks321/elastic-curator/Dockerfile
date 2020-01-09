FROM centos:7
MAINTAINER rasmus@aiotex.com

RUN mkdir /etc/curator
RUN mkdir /etc/curator/logs
COPY config/config.yml /etc/curator/config.yml
COPY config/actions.yml /etc/curator/actions.yml

# Install python-pip
RUN curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py"
RUN python get-pip.py

# Install curator (https://www.elastic.co/guide/en/elasticsearch/client/curator/4.2/installation.html)
RUN pip install elasticsearch-curator


# download go-cron
RUN curl -L -o /usr/local/bin/go-cron-linux.gz https://github.com/odise/go-cron/releases/download/v0.0.7/go-cron-linux.gz
RUN gunzip /usr/local/bin/go-cron-linux.gz
RUN chmod u+x /usr/local/bin/go-cron-linux

ENV PATH=/usr/local/bin:$PATH
# "0 0 4 * * ?" runs every day at 4 am
ENV SCHEDULE "0 0 4 * * ?"
ENV COMMAND "echo test go-cron"
EXPOSE 8080
CMD go-cron-linux -s "$SCHEDULE" -p 8080 -- /bin/bash -c "$COMMAND"