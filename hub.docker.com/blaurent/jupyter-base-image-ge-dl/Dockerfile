FROM tensorflow/tensorflow:1.12.0-gpu-py3 as builder

ENV LC_ALL C.UTF-8
ENV LANG C.UTF-8
ENV PYTHONDONTWRITEBYTECODE=1
# Seems to speed things up
ENV PYTHONUNBUFFERED=1
ENV PATH="/venv/bin:$PATH"

RUN apt-get -q update && apt-get install -qy --no-install-recommends python3-venv

# Setup the virtualenv
RUN python -m venv /venv

# Install Python deps
RUN pip install pipenv
COPY Pipfile Pipfile.lock ./
RUN pipenv install --system --deploy

RUN pip --no-cache-dir install --upgrade \
    pip \
    setuptools \
    pipenv


    
