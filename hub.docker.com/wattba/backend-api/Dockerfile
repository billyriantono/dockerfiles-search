FROM python:3.7-alpine
ADD . /app
WORKDIR /app
RUN apk update && \
	apk add --no-cache build-base python-dev && \
	pip install -r requirements.txt && \
    apk del build-base python-dev
ENTRYPOINT ["python"]
CMD ["app.py"]