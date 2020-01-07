# vim:set ft=dockerfile
FROM debian:jessie

# system update
RUN apt-get update \
    && apt-get upgrade -y

# Only installs ansible's minimal required dependencies.

RUN apt-get install -y \
    python-dev \
    python-pip  \
    libffi-dev \
    libssl-dev \
    sudo

RUN pip install --upgrade \
    ansible \
    setuptools \
    packaging \
    pyparsing \
    appdirs

# Execute ansible playbook(s).

COPY provisioning/ provisioning
RUN ansible-playbook provisioning/site.yml -c local

# Copy entrypoint.

COPY entrypoint.sh /
RUN chmod o+x ./entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
