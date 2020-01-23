FROM alpine
RUN apk update && apk add python py-pip git wget bash
RUN pip install speedtest-cli
RUN wget -O /bin/speedtest-csv https://raw.githubusercontent.com/HenrikBengtsson/speedtest-cli-extras/master/bin/speedtest-csv &&\
    chmod +x /bin/speedtest-csv
RUN git clone https://github.com/charlyhue/zspeedtest.git
WORKDIR zspeedtest
CMD ["python", "zspeedtest.py"]
