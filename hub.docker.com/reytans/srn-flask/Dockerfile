## Dockerfile - ex-py-docker-flask
##
FROM gcr.io/gcp-runtimes/ubuntu_16_0_4
RUN apt-get update -y && apt-get install -y python-pip python-dev build-essential && rm -rf /var/lib/apt/lists/*
RUN pip install Flask
COPY . /apt
WORKDIR /apt
RUN pip install -r requirements.txt
ENTRYPOINT ["python"]
CMD ["app.py"]
EXPOSE 5000
