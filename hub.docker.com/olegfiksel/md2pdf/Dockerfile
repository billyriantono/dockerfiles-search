FROM debian:wheezy

RUN apt-get update -y && apt-get install --no-install-recommends -y -q curl python build-essential git ca-certificates libfontconfig1
RUN mkdir /nodejs && curl http://nodejs.org/dist/v0.10.28/node-v0.10.28-linux-x64.tar.gz | tar xvzf - -C /nodejs --strip-components=1
ENV PATH $PATH:/opt/md2pdf:/nodejs/bin
RUN mkdir /opt/md2pdf && cd /opt/md2pdf && npm install markdown-pdf
COPY md2pdf.js md2pdf_all.sh /opt/md2pdf/
CMD ["/bin/bash"]
