FROM alecx/golang-build AS builder

WORKDIR /build
COPY ./backend .

# run tests
# add .mongo file or env MONGO_TEST with mongo url for tests agains real mongodb server
RUN \
    if [ -f .mongo ] ; then export MONGO_TEST=$(cat .mongo) ; fi && \
    cd app && \
    if [ -z "$SKIP_TEST" ] ; then \
        go test -mod=vendor -covermode=count -coverprofile=/profile.cov_tmp ./... && \
        cat /profile.cov_tmp > /profile.cov ; \
    else echo "skip tests" ; fi

RUN echo "mongo=${MONGO_TEST}" >> /etc/hosts

# linters
RUN if [ -z "$SKIP_TEST" ] ; then \
    if [ -f .mongo ] ; then export MONGO_TEST=$(cat .mongo) ; fi && \
        golangci-lint run --out-format=tab --disable-all --tests=false --enable=unconvert \
        --enable=megacheck --enable=structcheck --enable=gas --enable=gocyclo --enable=dupl --enable=misspell \
        --enable=unparam --enable=varcheck --enable=deadcode --enable=typecheck \
        --enable=ineffassign --enable=varcheck ./... ; \
    else echo "skip linters" ; fi

# submit coverage to coverals if COVERALLS_TOKEN in env
RUN if [ -z "$COVERALLS_TOKEN" ] ; then \
    echo "coverall not enabled" ; \
    else goveralls -coverprofile=/profile.cov -service=travis-ci -repotoken $COVERALLS_TOKEN || echo "coverall failed!"; fi


RUN cd app && CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -mod vendor -o /build/server

FROM alpine:3.9
COPY --from=builder /build/server /srv/server
ENTRYPOINT ["/srv/server"]
