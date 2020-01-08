FROM python:alpine

RUN pip install Flask==0.12.2

RUN mkdir -p /opt/project
WORKDIR /opt/project

ENV FLASK_APP=hello.py

COPY hello.py /opt/project/hello.py

EXPOSE 5000

CMD ["flask", "run", "--host", "0.0.0.0", "--port", "5000"]
