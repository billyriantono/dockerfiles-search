FROM debian:9-slim
RUN apt-get update && apt-get install -yy python3 python3-pip wget git
RUN apt-get clean
RUN git clone https://github.com/xgi/castero
RUN cd /castero && git checkout d897ddc309c390c4661b477bc99dec6636404ccc
RUN cd /castero && python3 setup.py install
ENTRYPOINT ["castero"]

