FROM python:3.7-alpine
ADD ./src/req.txt /tmp/req.txt
RUN pip install -qr /tmp/req.txt
ADD ./src /opt/src/
WORKDIR /opt/src
EXPOSE 5000
CMD ["python", "app.py"]