FROM kasured/akka-cluster-bin
MAINTAINER Evgeny Rusak "kasured@gmail.com"

ENV HTTP_SERVICE_HOST=127.0.0.1 HTTP_SERVICE_PORT=8080 CLUSTER_CLIENT_SYSTEM_PORT=0 CLUSTER_CLIENT_SYSTEM_HOST=127.0.0.1 CLUSTER_CONTACT_POINTS=

CMD ["http_service/target/universal/stage/bin/http-service"]
