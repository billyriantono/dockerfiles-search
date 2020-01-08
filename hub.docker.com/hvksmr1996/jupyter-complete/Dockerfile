FROM ubuntu:18.10

ENV PATH="/root/.local/bin:/root/bin:/.local/bin:/local/bin:${PATH}"

ADD scripts /usr/bin
RUN chmod +x /usr/bin/*.sh

RUN install-deb.sh
RUN install-jupyter.sh
RUN install-haskell.sh

EXPOSE 8888
CMD [ "main.sh" ]
