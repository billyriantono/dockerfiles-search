FROM python:3

ADD requirements.txt /App/

RUN apt-get update
RUN pip install jupyter -r App/requirements.txt

CMD jupyter notebook --ip 0.0.0.0 --port 8888 --no-browser --allow-root