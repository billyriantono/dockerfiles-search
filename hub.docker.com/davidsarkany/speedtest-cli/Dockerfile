FROM python:alpine
RUN wget -O /usr/local/bin/speedtest https://raw.githubusercontent.com/sivel/speedtest-cli/master/speedtest.py && chmod +x /usr/local/bin/speedtest
ENTRYPOINT ["python","/usr/local/bin/speedtest"]
