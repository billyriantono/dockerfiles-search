FROM ubuntu:latest

LABEL "name"="Builder"
LABEL "maintainer"="Andrew Hayes <andrew@1eq.me>"
LABEL "version"="1.0.0"

LABEL "com.github.actions.icon"="package"
LABEL "com.github.actions.color"="blue"
LABEL "com.github.actions.name"="Build Lambda"
LABEL "com.github.actions.description"="####todo####"
COPY LICENSE README.md /

COPY Build.sh /

RUN sh /Build.sh

#ENTRYPOINT [".github/Run.sh"]
ENTRYPOINT ["/bin/sh"]

