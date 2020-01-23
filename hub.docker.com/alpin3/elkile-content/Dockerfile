FROM python:3-slim

WORKDIR /api

COPY . /api

RUN pip install --trusted-host pypi.python.org -r requirements.txt

EXPOSE 5000

CMD ["python", "src/main.py"]