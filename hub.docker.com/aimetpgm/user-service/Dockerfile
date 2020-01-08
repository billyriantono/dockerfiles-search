FROM python:2-onbuild

ADD userservice.py /
ADD requirements.txt /

#RUN virtualenv project
#RUN source project/bin/activate
RUN pip install -r requirements.txt

CMD [ "python", "./userservice.py" ]
