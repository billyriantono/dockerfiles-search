FROM python:latest

COPY src /src

WORKDIR /src

RUN pip install -r requirements.txt \
    && groupadd -r flask \
    && useradd -r -g flask flask

EXPOSE 5000

USER flask

#CMD ["python", "main.py"]
