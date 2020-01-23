FROM google/cloud-sdk:latest

RUN chmod +x /usr/lib/google-cloud-sdk/platform/google_appengine/appcfg.py && \
    ln -s /usr/lib/google-cloud-sdk/platform/google_appengine/appcfg.py /usr/bin/appcfg.py 
RUN mkdir /data
ENV GOPATH /data