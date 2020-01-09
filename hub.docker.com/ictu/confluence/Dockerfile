FROM cptactionhank/atlassian-confluence

USER root

RUN    apt-get update \
    && apt-get install -y graphviz \
    && apt-get clean

USER daemon:daemon
