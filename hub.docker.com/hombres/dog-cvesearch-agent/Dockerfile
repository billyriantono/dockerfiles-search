FROM alpine:latest
RUN apk update && apk add python py-pip python-dev linux-headers alpine-sdk nmap
RUN mkdir -p /opt/dog/agents
ADD ./cve_search.py /opt/dog/agents/cve_search.py
ADD ./requirements.txt /opt/dog/agents/requirements.txt
RUN pip install -r /opt/dog/agents/requirements.txt
ADD ./start.sh /opt/dog/agents/start.sh
RUN chmod +x /opt/dog/agents/start.sh
CMD ["/opt/dog/agents/start.sh", "cve_search"]
