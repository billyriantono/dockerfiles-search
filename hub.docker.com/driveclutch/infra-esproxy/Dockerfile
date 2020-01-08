FROM nginx:1.11-alpine
MAINTAINER David Hallum <david@driveclutch.com>

ENV ES_ENDPOINT "localhost:65535"
ENV ES_SCHEME "http"

COPY nginx.conf_template /etc/nginx/nginx.conf_template

CMD /bin/sh -c "envsubst '\${ES_ENDPOINT} \${ES_SCHEME}' < /etc/nginx/nginx.conf_template > /etc/nginx/nginx.conf && nginx -g 'daemon off;'"
