FROM python:3.7.3-stretch

RUN useradd --create-home codewarrior

RUN set -ex; \
    apt-get update; \
    apt-get install -y --no-install-recommends \
        libblas-dev \
        liblapack-dev \
        gfortran \
# For gmpy2
        libgmp-dev \
        libmpc-dev \
        libmpfr-dev \
    ; \
    rm -rf /var/lib/apt/lists/*;

# Install poetry (https://github.com/sdispater/poetry) globally like Arch Linux
# https://git.archlinux.org/svntogit/community.git/tree/trunk?h=packages/poetry
COPY rootfs/usr/local/bin/poetry /usr/local/bin/poetry
RUN set -ex; \
    mkdir -p /opt/poetry; \
    curl -sSL https://github.com/sdispater/poetry/releases/download/0.12.12/poetry-0.12.12-linux.tar.gz | tar xz -C /opt/poetry; \
    chmod +x /usr/local/bin/poetry; \
    poetry --version;

RUN set -ex; \
    mkdir -p /workspace/default; \
    chown -R codewarrior:codewarrior /workspace;

COPY --chown=codewarrior:codewarrior rootfs/workspace/default/pyproject.toml /workspace/default/pyproject.toml
COPY --chown=codewarrior:codewarrior rootfs/workspace/default/poetry.lock /workspace/default/poetry.lock
COPY --chown=codewarrior:codewarrior rootfs/workspace/django/pyproject.toml /workspace/django/pyproject.toml
COPY --chown=codewarrior:codewarrior rootfs/workspace/django/poetry.lock /workspace/django/poetry.lock

USER codewarrior
RUN set -ex; \
    cd /workspace/default; \
    python -m venv --symlinks .; \
    VIRTUAL_ENV=/workspace/default poetry install; \
    cd /workspace/django; \
    python -m venv --symlinks .; \
    VIRTUAL_ENV=/workspace/django poetry install;

WORKDIR /workspace
