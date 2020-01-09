FROM alpine:latest
RUN apk update && apk add python py-pip python-dev linux-headers alpine-sdk nikto
RUN mkdir -p /opt/dog/agents
ADD ./nikto_agent.py /opt/dog/agents/nikto_agent.py
ADD ./requirements.txt /opt/dog/agents/requirements.txt
RUN pip install -r /opt/dog/agents/requirements.txt
ADD ./start.sh /opt/dog/agents/start.sh
RUN chmod +x /opt/dog/agents/start.sh
CMD ["/opt/dog/agents/start.sh", "nikto_agent"]
