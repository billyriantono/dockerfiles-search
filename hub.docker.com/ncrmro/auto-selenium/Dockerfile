FROM python:3.6-alpine
WORKDIR /app
ARG SERVER_URL=http://serve:5000
ARG SELENIUM_URL=http://selenium_hub:4444/wd/hub

COPY requirements.txt requirements.txt
RUN pip3 install -r ./requirements.txt

COPY ./*.py /app
#RUN python3 ./selenium_compiler.py --server_url=$SERVER_URL --selenium_url=$SELENIUM_URL

ENTRYPOINT ["python3"]
CMD ["-m", "unittest", "discover", "--start-directory", "__tests__", "--pattern", "test_*_compiled.py"]
