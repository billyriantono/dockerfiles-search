FROM frolvlad/alpine-python2
ENV AWS_DEFAULT_REGION us-west-2
EXPOSE 5000
ADD ./app /app
WORKDIR /app
VOLUME /scheduler
RUN pip install -r requirements.txt
ENTRYPOINT python main.py
