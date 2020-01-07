FROM python:3.5
RUN mkdir /ldo
COPY . /ldo
WORKDIR /ldo
RUN pip3 install -r requirements.txt
RUN pip3 install uwsgi
EXPOSE 3031
CMD ["uwsgi", "--master", "--ini", "loco.ini"]