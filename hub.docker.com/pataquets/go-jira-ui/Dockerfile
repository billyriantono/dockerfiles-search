FROM golang

RUN \
  apt-get update && \
  DEBIAN_FRONTEND=noninteractive \
    apt-get install -y \
      nano \
      vim \
  && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/

RUN go get -v github.com/mikepea/go-jira-ui/jira-ui

ENTRYPOINT [ "jira-ui" ]
