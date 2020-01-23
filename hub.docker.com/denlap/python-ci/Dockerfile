FROM alpine:3.4

RUN apk add --no-cache python3 && \ 
python3 -m ensurepip && \ 
rm -r /usr/lib/python*/ensurepip && \ 
pip3 install --upgrade pip setuptools && \ 
rm -r /root/.cache

COPY test.py /app/test.py

CMD ["python3", "/app/test.py"]
