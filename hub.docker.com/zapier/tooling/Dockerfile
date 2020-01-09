FROM python:3.7.3-slim-stretch

# Docker

RUN apt-get update && \
    apt-get install -y apt-transport-https ca-certificates \
    curl gnupg2 software-properties-common zip && \
	curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - && \
	add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable" && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean && \
    apt-get purge -y

RUN apt-get update && \
    apt-get install -y docker-ce docker-ce-cli containerd.io && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean && \
    apt-get purge -y

RUN curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" \
    -o /usr/local/bin/docker-compose && \
	chmod +x /usr/local/bin/docker-compose

# Python

RUN apt-get update && \
apt-get install -yq --no-install-recommends \
build-essential libpq-dev python-pip libffi-dev python3-dev git curl && \
pip install --upgrade pip requests && \
rm -rf /var/lib/apt/lists/* && \
apt-get clean && \
apt-get purge -y

# Poetry

ENV POETRY_VERSION=1.0.0
RUN curl -sSL https://raw.githubusercontent.com/sdispater/poetry/master/get-poetry.py | python
ENV PATH="/root/.poetry/bin:${PATH}"

# GitLab

COPY track_gitlab_event.py /usr/local/bin/track-gitlab-event
RUN chmod a+x /usr/local/bin/track-gitlab-event

# Workspace

ENV PYTHONDONTWRITEBYTECODE true

# Validation

COPY verchew.ini /opt/
RUN pip install verchew
CMD verchew --root=/opt/ --exit-code
