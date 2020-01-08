FROM google/cloud-sdk:latest

# Install gettext, contains the envsubst command, for env vars substitution
# Also install python3 and Jinja2, needed for Kubernetes templating
# Aswell as libyaml for pyaml and jinja2-cli for cli jinka tools
RUN apt-get install -y gettext python3-pip libyaml-dev
RUN pip3 install Jinja2
RUN pip3 install PyYAML
RUN pip3 install jinja2-cli

# Install stack, and add its binaries to PATH
# Also install dhall and various utilities
ENV PATH="/root/.local/bin:${PATH}"
RUN curl -sSL https://get.haskellstack.org/ | sh
RUN stack setup
# Patching this issue: https://github.com/commercialhaskell/intero/issues/372#issuecomment-282524845
RUN ln -s /lib/x86_64-linux-gnu/libtinfo.so.5 /lib/x86_64-linux-gnu/libtinfo.so
RUN stack install dhall dhall-json dhall-text
