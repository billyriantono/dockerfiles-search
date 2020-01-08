FROM mobz/elasticsearch-head:5-alpine

ENV ES_PATH=localhost:9200

CMD sed -i "s/localhost:9200/${ES_PATH}/g" /usr/src/app/_site/app.js &&\
    sed -i "s/^.uiNodesView-nullReplica,/.uiNodesView-nullReplica { display: none; } /g" /usr/src/app/_site/app.css &&\
    node_modules/http-server/bin/http-server _site -p 9100
