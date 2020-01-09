FROM python:3.7.4-alpine3.10

ENV PYTHONFAULTHANDLER=1 \
    PYTHONHASHSEED=random \
    PYTHONUNBUFFERED=1 \
    PIP_DEFAULT_TIMEOUT=100 \
    PIP_DISABLE_PIP_VERSION_CHECK=1 \
    PIP_NO_CACHE_DIR=1 \
    POETRY_VERSION=1.0.0

WORKDIR /app
COPY requirements.txt ./
RUN pip install -r ./requirements.txt
COPY dns_update.py ./

ENTRYPOINT ["python", "./dns_update.py"]
