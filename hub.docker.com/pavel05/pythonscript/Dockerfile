FROM python:3.6
RUN mkdir /code
WORKDIR /code
ADD requirements.txt /code/
RUN pip install -r requirements.txt
ENTRYPOINT ["bash", "/code/bootstrap.sh"]
