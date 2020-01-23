FROM python:3.7-alpine as builder
ENV PYTHONUNBUFFERED 1
ADD requirements.txt /
RUN pip install -r /requirements.txt \
 && rm /requirements.txt \
 && mkdir -p /app
WORKDIR /app

FROM gcr.io/distroless/python3
COPY --from=builder /usr/local/lib/python3.7/site-packages /site-packages
ENV PYTHONPATH=/site-packages
WORKDIR /app
HEALTHCHECK CMD ["/usr/bin/python", "-V"]