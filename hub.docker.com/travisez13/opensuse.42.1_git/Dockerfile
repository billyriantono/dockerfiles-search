FROM opensuse:42.1
LABEL maintainer='Travis Plunk <github@ez13.net>'
LABEL readme.md="https://github.com/TravisEz13/docker/blob/master/opensuse/42.1/git/readme.md"
LABEL description="This Dockerfile for OpenSUSE 42.1 with git."

RUN zypper --non-interactive update --skip-interactive \
    && zypper --non-interactive install \
        git \
    && zypper --non-interactive clean --all 

ENTRYPOINT [ "bash" ]
