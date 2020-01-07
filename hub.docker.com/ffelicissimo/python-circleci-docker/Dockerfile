FROM python:2.7.14

RUN mkdir -p /opt/hello_word/
WORKDIR /opt/hello_word/

COPY requirements.txt .
COPY hello_world.py .

RUN pip install -r requirements.txt

EXPOSE 80

ENTRYPOINT ["python", "/opt/hello_word/hello_world.py"]
