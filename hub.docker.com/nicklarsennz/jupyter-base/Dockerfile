FROM ubuntu:bionic

RUN apt update && \
    apt install -y python3.7 python3-pip && \
    update-alternatives --install /usr/bin/pip pip /usr/bin/pip3 1 && \
    pip install --upgrade pip

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

EXPOSE 8080

ENTRYPOINT ["jupyter", "lab"]