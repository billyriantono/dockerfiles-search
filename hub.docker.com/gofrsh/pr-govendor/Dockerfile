FROM gofrsh/pr-base:latest

FROM koalaman/shellcheck-alpine

COPY --from=0 /opt/github.sh /opt/
COPY govendor.sh /opt/

RUN set -x \
    && shellcheck /opt/*.sh

FROM gofrsh/pr-base:latest

RUN set -x \
    && go get -u github.com/kardianos/govendor \
    && govendor --version

COPY govendor.sh /opt/

# TODO: add a stepdown?
ENTRYPOINT ["/opt/govendor.sh"]
