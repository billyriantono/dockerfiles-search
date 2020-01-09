FROM python:2

RUN apt-get update && apt-get install -y git-core bash sudo clang python-pip wget clang libpcap-dev && git clone https://github.com/leviathan-framework/leviathan.git

WORKDIR leviathan
RUN bash scripts/debian_install.sh
ENTRYPOINT [ "bash" ]
