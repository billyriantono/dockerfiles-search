FROM python:3.6-slim

WORKDIR /app
COPY . /app
EXPOSE 8182
RUN apt-get update -y && apt-get install -y python-pip
RUN pip3 install pipenv==8.3.1 && pipenv install --deploy --system

RUN groupadd -g 993 commstemplatesvc && \
    useradd -r -u 993 -g commstemplatesvc commstemplatesvc
USER commstemplatesvc

ENTRYPOINT ["python3"]
CMD ["run.py"]
