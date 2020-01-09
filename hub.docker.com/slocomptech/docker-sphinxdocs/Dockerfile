FROM python:slim-stretch

# Shell
SHELL ["/bin/bash","-c"]

# Get updates install dependencies
RUN apt-get update && apt-get install git make -y && apt-get clean && rm -rf /var/lib/apt/list/* && \
    pip install -U sphinx && \
    pip install recommonmark && \
    pip install sphinx_rtd_theme && \
    pip install sphinx_bootstrap_theme && \
    pip install guzzle_sphinx_theme