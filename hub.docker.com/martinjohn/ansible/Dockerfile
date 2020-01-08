FROM python:3

RUN pip install --no-cache-dir ansible

WORKDIR /src

ENTRYPOINT ["ansible-playbook"]
CMD ["--help"]

