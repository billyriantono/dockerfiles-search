FROM python:3
ENV PYTHONUNBUFFERED 1
RUN mkdir /code
WORKDIR /code
COPY requirements.txt /code/
RUN pip install django-widget-tweaks
RUN python3 -m pip install Pillow
RUN pip install -r requirements.txt
COPY . /code/