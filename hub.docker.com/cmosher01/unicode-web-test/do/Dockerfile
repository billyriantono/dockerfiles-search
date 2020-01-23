FROM python:3.6

WORKDIR /administration

COPY requirements.txt /administration
RUN pip install -r requirements.txt

COPY administration.py /administration
CMD python administration.py