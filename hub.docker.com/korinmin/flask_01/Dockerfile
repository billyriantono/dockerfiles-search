FROM python:3.6.8

RUN pip install Flask==1.0.2 && \
pip install datetime
COPY . /

ENV FLASK_APP=hello.py
EXPOSE 5000

CMD ["flask", "run", "--host=0.0.0.0"]