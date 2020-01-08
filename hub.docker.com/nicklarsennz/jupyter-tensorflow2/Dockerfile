FROM python:3.7-slim

ARG USER=jupyter
ARG UID=1000

ENV EXTERNAL_HOST=localhost
ENV EXTERNAL_PORT=8080

RUN useradd -m -s /bin/bash -N -u ${UID} ${USER} && \
    mkdir /data && \
    chown -R ${USER} /data

USER ${USER}
WORKDIR /home/${USER}

RUN mkdir -p .jupyter/lab

COPY requirements.txt .
COPY config.py ./.jupyter/jupyter_notebook_config.py
ENV PATH=/home/${USER}/.local/bin:${PATH}
RUN pip install --user -r requirements.txt
RUN whoami

ENTRYPOINT ["jupyter", "lab"]