FROM python:2.7.14

COPY magic.py /magic.py

RUN chmod +x /magic.py

EXPOSE 8888/udp

CMD ["python", "-u" ,"/magic.py"]
