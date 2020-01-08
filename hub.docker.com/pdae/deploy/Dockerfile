FROM debian:latest

RUN apt-get update && apt-get install -y openssh-client zip curl unoconv

RUN mkdir -p ~/.ssh && \
     /bin/echo -e "Host *\n\tStrictHostKeyChecking no\n\n" > ~/.ssh/config

COPY pack /usr/local/bin/
RUN chmod +x /usr/local/bin/pack

COPY put /usr/local/bin/
RUN chmod +x /usr/local/bin/put
