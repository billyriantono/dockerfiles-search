FROM python:3-alpine
ARG VERSION=fac8e4274fdcee90ce52e42e70aa5639486a5013
RUN apk add --no-cache git && pip install https://codeload.github.com/josegonzalez/python-github-backup/tar.gz/$VERSION
ENTRYPOINT ["/usr/local/bin/github-backup"]
CMD ["--help"]
