FROM python:3.7
ENV PYTHONUNBUFFERED 1
WORKDIR /usr/src/app

RUN pip install --no-cache-dir pandas==0.23.4
RUN pip install --no-cache-dir pandas-datareader
RUN pip install virtualenv
RUN virtualenv ENV
RUN /bin/bash -c "source ENV/bin/activate"
RUN pip install Django==2.1
RUN pip install numpy==1.15.1
RUN pip install bokeh==0.13.0
RUN pip install scipy==1.1.0

COPY . .

RUN python manage.py migrate
RUN python manage.py collectstatic

EXPOSE 8000

CMD python manage.py runserver 0.0.0.0:8000