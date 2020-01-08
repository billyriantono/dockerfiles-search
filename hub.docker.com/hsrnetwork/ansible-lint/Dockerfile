FROM python:3-slim
LABEL maintainer="Yannick Zwicker <yzwicker@ins.hsr.ch>"

WORKDIR /work

RUN pip3 install yamllint ansible-lint

CMD ["ansible-lint", "--help"]