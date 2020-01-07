FROM circleci/golang
USER root

RUN apt-get update && apt-get install -y jq

ENV TEST_RESULTS /tmp/test-results
RUN mkdir -p $TEST_RESULTS \
 && chmod 755 $TEST_RESULTS \
 && chown -R circleci:circleci $TEST_RESULTS

RUN go get \
  github.com/jstemmer/go-junit-report \
  golang.org/x/tools/cmd/cover \
  github.com/mattn/goveralls

USER circleci
