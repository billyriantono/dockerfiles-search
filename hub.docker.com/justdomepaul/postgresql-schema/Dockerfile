FROM justdomepaul/migration:no-entry
RUN apk add --no-cache curl bash postgresql-client
ADD ./migrations ./migrations
ADD ./database ./database
ADD ./control.sh ./control.sh
RUN chmod u+x ./control.sh

CMD ["top", "-b"]
