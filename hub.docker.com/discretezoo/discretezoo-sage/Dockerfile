# Dockerfile for binder
# Reference: https://mybinder.readthedocs.io/en/latest/dockerfile.html#preparing-your-dockerfile

FROM sagemath/sagemath:8.6

USER root
RUN    apt-get update -qq \
    && apt-get install -y git wget \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

USER sage
RUN git clone --recursive https://github.com/DiscreteZOO/DiscreteZOO-sage.git ${HOME}/DiscreteZOO-sage
RUN mkdir ${HOME}/.discretezoo
RUN wget https://data.discretezoo.xyz/discretezoo.db -O ${HOME}/.discretezoo/discretezoo.db -q
RUN ln -s ${HOME}/DiscreteZOO-sage/discretezoo ${HOME}/sage/local/lib/python2.7/site-packages/discretezoo
RUN sage -pip install psycopg2-binary
