# kentwait/miniconda:python3
FROM kentwait/alpine-glibc-base
MAINTAINER Kent Kawashima <kentkawashima@gmail.com>

ENV CONDA_PYTHON_VERSION 3
ENV CONDA_DIR /opt/conda
# Latest version 4.3.11 as of 2017-02-14  
ENV CONDA_VERSION latest  
ENV PATH ${CONDA_DIR}/bin:${PATH}

WORKDIR /tmp
RUN apk update && apk upgrade \
  && apk add --no-cache --virtual temp-pkgs \
    build-base \
    ca-certificates \
    wget \
    python \
  # Install Miniconda
  && wget -q "https://repo.continuum.io/miniconda/Miniconda${CONDA_PYTHON_VERSION}-${CONDA_VERSION}-Linux-x86_64.sh" -O /tmp/installer.sh \
  && bash installer.sh -b -p ${CONDA_DIR} \
  # remove packages and clean up 
  && apk del temp-pkgs \
  && find /opt -name __pycache__ | xargs rm -r \
  && rm -rf /tmp/* \
            /var/cache/apk/* \
            /opt/conda/pkgs/* \
            /root/.wget-hsts \
            /root/.[acpw]*

WORKDIR /
ENTRYPOINT ["/init"]
CMD ["python"]