FROM docker.io/sshnaidm/python3:latest
LABEL maintainer "sshnaidm <einarum@gmail.com>"
LABEL name "testimage"

COPY requirements.txt /requirements.txt
# Uncomment in case you want to include app in container
#COPY app /app
RUN pip3 install --upgrade -r /requirements.txt

WORKDIR /app
EXPOSE 5000

CMD ["python", "app.py"]
