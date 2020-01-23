FROM alpine:latest

LABEL version="1.0.0"
LABEL repository="https://github.com/cirruslabs/actions-rebase"
LABEL homepage="https://github.com/cirruslabs/actions-rebase"
LABEL maintainer="Cirrus Labs"
LABEL "com.github.actions.name"="PR Rebase"
LABEL "com.github.actions.description"="Rebase PRs with rebase_required label"
LABEL "com.github.actions.icon"="check"
LABEL "com.github.actions.color"="black"

RUN apk --no-cache add jq git

ADD rebase.sh /usr/bin/rebase

ENTRYPOINT ["rebase"]