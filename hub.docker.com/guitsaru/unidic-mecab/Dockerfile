FROM python:3

RUN apt-get update && \
  apt-get install -y --no-install-recommends libmecab2 libmecab-dev unidic-mecab && \
  rm -rf /var/lib/apt/lists/*