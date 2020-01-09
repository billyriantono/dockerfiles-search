FROM python:3.6

RUN mkdir /opt/jblythe
WORKDIR /opt/jblythe

#Pull Code
RUN git clone https://github.com/jblythe/myapp.git

RUN pip install -r myapp/requirements.txt
CMD python myapp/app.py
