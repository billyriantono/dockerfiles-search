FROM robosearcherdock/service_base:01

ENV PYTHONUNBUFFERED 1

ADD . /python_indicator_builder

WORKDIR /python_indicator_builder

ENV PYTHONPATH /python_indicator_builder

EXPOSE 7007
EXPOSE 8008

ENV PYTHONPATH /python_indicator_builder

CMD ["python", "/python_indicator_builder/app.py"]