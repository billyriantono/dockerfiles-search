FROM linkyard/docker-helm

RUN apk add --no-cache bash curl
RUN helm init --client-only
RUN helm plugin install --version master https://github.com/sonatype-nexus-community/helm-nexus-push.git
