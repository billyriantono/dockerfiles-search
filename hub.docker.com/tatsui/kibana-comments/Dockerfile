ARG VERSION
FROM docker.elastic.co/kibana/kibana-oss:${VERSION}
ARG VERSION
RUN kibana-plugin install https://github.com/gwintzer/kibana-comments-app-plugin/releases/download/${VERSION}/kibana-comments-app-plugin-${VERSION}-1.zip
