FROM python:3.6

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

COPY backend/physio-backend/requirements.txt /usr/src/app/

RUN pip install --no-cache-dir -r requirements.txt
RUN python -m pip install --upgrade https://storage.googleapis.com/tensorflow/mac/cpu/tensorflow-0.12.0-py3-none-any.whl

COPY backend/physio-backend /usr/src/app

RUN mkdir -p /usr/src/app/static/

ADD frontend/arkathon-frontend/dist/arkathon-frontend /usr/src/app/static

EXPOSE 8080

ENTRYPOINT ["python"]

CMD ["-m", "swagger_server"]
