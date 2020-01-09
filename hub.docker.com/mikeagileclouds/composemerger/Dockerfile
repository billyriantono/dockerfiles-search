FROM python:3

RUN pip3 install pyyaml

COPY src /app/

ENTRYPOINT [ "python3", "/app/merger.py" ]
