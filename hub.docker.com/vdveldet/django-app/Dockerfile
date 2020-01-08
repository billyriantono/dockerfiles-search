FROM python:3.6
RUN mkdir /code
WORKDIR /code

# set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

ADD requirements.txt /code/
RUN pip install --no-cache-dir -r requirements.txt

# copy project
COPY code/ /code

COPY ./entrypoint.sh /code/entrypoint.sh
RUN chmod +x /code/entrypoint.sh

# outsite port
EXPOSE 8000

# run entrypoint.sh
ENTRYPOINT ["/code/entrypoint.sh"]
