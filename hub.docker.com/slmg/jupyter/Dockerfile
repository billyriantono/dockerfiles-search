FROM ubuntu:bionic

RUN useradd -m moby -u 1000

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        python3 \
        python3-venv \
        python3-dev && \
    rm -rf /var/lib/apt/lists/*

USER moby
WORKDIR /home/moby

ENV VIRTUAL_ENV /home/moby/.venv
ENV PATH ${VIRTUAL_ENV}/bin:${PATH}

RUN python3 -m venv ${VIRTUAL_ENV} && \
    pip install --upgrade --no-cache-dir \
        pip && \
    pip install --no-cache-dir \
        jupyter \
        jupytext && \
    mkdir /home/moby/notebooks

COPY --chown=moby:moby config .jupyter/

EXPOSE 8888

CMD [ "jupyter", "notebook" ]
