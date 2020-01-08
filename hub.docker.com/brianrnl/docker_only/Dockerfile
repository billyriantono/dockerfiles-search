FROM openwhisk/dockerskeleton

ENV FLASK_PROXY_PORT 8080

# Install dependencies
ADD requirements.txt /action/requirements.txt
RUN cd /action; pip install -r requirements.txt


CMD ["/bin/bash", "-c", "cd actionProxy && python -u actionproxy.py"]
