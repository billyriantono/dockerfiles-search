FROM justdomepaul/migration:no-entry
RUN apk add --no-cache curl bash py-pip
RUN bash -c "python <(curl https://bootstrap.pypa.io/get-pip.py)"; \
    pip install cqlsh && \
    mkdir /root/.cassandra

ADD ./cqlshrc ./root/.cassandra/cqlshrc

ADD ./keyspace ./keyspace
ADD ./migrations ./migrations
ADD ./control.sh ./control.sh
RUN chmod u+x ./control.sh


CMD ["top", "-b"]
