FROM mongo

ADD entrypoint.sh .
ADD setup-replicaset.js .

EXPOSE 27017

CMD bash entrypoint.sh
