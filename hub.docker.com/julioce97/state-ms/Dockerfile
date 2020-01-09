FROM python:3.7.4

ENV PYTHONUNBUFFERED 1
RUN mkdir /pugchat-status
WORKDIR /pugchat-status
COPY . /pugchat-status/
RUN pip install -r requirements.txt
CMD ["bash","-c","sleep 40 && python pugchat-status/manage.py migrate && python pugchat-status/manage.py runserver 0.0.0.0:8000"]
#CMD ["python","pugchat-status/manage.py","runserver","0.0.0.0:8000"]
EXPOSE 8000
