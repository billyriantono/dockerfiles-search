FROM alpine:latest

ENV TOOLS_HOME /opt/tools

WORKDIR /root

# Install pipeline tools
ARG TOOL="git-merge-master"
COPY ./tools/${TOOL} ${TOOLS_HOME}/
RUN chmod +x ${TOOLS_HOME}/${TOOL}

ARG TOOL="is-pr"
COPY ./tools/${TOOL} ${TOOLS_HOME}/
RUN chmod +x ${TOOLS_HOME}/${TOOL}

ARG TOOL="node-coverage"
COPY ./tools/${TOOL} ${TOOLS_HOME}/
RUN chmod +x ${TOOLS_HOME}/${TOOL}