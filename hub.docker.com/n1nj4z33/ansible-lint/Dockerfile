FROM python:3-slim
MAINTAINER n1nj4z33 <n1nj4z33@gmail.com>

RUN pip install \
    ansible==2.7.9 \
    ansible-lint==4.1.0 \
    yamllint==1.15.0 \
    && rm -rf /root/.cache/pip

WORKDIR /work

COPY entrypoint.py /usr/local/bin

CMD ["python", "/usr/local/bin/entrypoint.py"]
