FROM python:3

RUN pip install boto3

WORKDIR /src

COPY . /src

CMD ["python3", "./insert_records_to_dynamodb_table.py"]

