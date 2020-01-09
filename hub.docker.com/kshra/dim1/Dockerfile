from python:3.7.4-buster

workdir /root

copy requirements.txt .

run \
      pip \
      install \
      --no-cache-dir \
      -r requirements.txt \
      && \
      rm -f requirements.txt \
      && \
      :

ENTRYPOINT ["python3"]
