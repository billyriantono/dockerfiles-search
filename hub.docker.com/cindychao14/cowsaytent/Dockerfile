FROM python:3.7-alpine

WORKDIR /home/root/block-checker

ADD ./requirements.txt /home/root/block-checker/requirements.txt
RUN pip install -r requirements.txt

ADD . /home/root/block-checker

CMD ["python", "src/block-checker.py"]
