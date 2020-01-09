FROM alpine:latest

MAINTAINER OSO DevOps (https://github.com/osodevops)

RUN apk add --update python py-pip git

#force fresh git clone each build.
ADD https://api.github.com/repos/osodevops/wafw00f/git/refs/heads/master version.json
RUN git clone https://github.com/osodevops/wafw00f

WORKDIR wafw00f

RUN python setup.py install

ENTRYPOINT ["wafw00f"]

CMD ["--help"]