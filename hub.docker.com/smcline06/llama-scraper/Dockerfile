FROM golang:1.13.3

WORKDIR /go/src/app

RUN go get -d -v github.com/dropbox/llama
RUN go install -v github.com/dropbox/llama/cmd/scraper

# A comma-separated list of IP addresses or hostnames where collectors can be reached
ENV COLLECTOR_HOSTS=127.0.0.1
# port on which the collector's API is configured to listen, 8100 is default
ENV COLLECTOR_PORT=8100
# influxDB hostname or ip address
ENV INFLUXDB_HOST=127.0.0.1
# influxdb database name
ENV INFLUXDB_NAME=llama
# influxdb listening port
ENV INFLUXDB_PORT=5000
# influxdb username
ENV INFLUXDB_USER=user
# influxdb password
ENV INFLUXDB_PASS=password
# llama polling interval in seconds
ENV INTERVAL=30

# Disabled influxdb authentication
CMD ["sh", "-c", "scraper -llama.collector-hosts $COLLECTOR_HOSTS -llama.collector-port $COLLECTOR_PORT -llama.influxdb-host $INFLUXDB_HOST  -llama.influxdb-name $INFLUXDB_NAME -llama.influxdb-port $INFLUXDB_PORT -llama.interval $INTERVAL"]

# Enabled influxdb authentication
#CMD ["sh", "-c", "scraper -llama.collector-hosts $COLLECTOR_HOSTS -llama.collector-port $COLLECTOR_PORT -llama.influxdb-host $INFLUXDB_HOST  -llama.influxdb-name $INFLUXDB_NAME -llama.influxdb-pass $INFLUXDB_PASS -llama.influxdb-port $INFLUXDB_PORT -llama.influxdb-user $INFLUXDB_USER -llama.interval $INTERVAL"]
