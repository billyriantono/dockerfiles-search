FROM multiarch/debian-debootstrap:arm64-sid-slim

RUN apt-get update \
  && apt-get -y install bash autoconf g++ git python-dev python-pip python-pbkdf2 \
  && cd / && git clone https://github.com/binux/qiandao.git && pip install --no-cache-dir -r /qiandao/requirements.txt \ 

  && apt-get purge -y --auto-remove autoconf g++ git \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /qiandao

VOLUME ["/qiandao/"]

ENV PORT 80
EXPOSE $PORT/tcp

CMD ["python","/qiandao/run.py"]