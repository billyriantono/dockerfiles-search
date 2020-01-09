FROM python:3.7-alpine
LABEL Autor="Alexey Morozov <iphosgen@ya.ru>"
LABEL Description="Test task Flask service"


# Init virtualenv
RUN python -m venv venv && \
    source venv/bin/activate && \
    pip install flask requests

COPY . /src
WORKDIR /src

EXPOSE 5000
ENTRYPOINT ["python3"]

CMD ["flask run"]