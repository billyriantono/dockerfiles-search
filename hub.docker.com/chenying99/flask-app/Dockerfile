FROM python:alpine

LABEL maintainer="Jeeva S. Chelladhurai"

COPY . /app
WORKDIR /app
RUN pip install -r requirements.txt
EXPOSE 5000
ENTRYPOINT ["python", "run.py"]