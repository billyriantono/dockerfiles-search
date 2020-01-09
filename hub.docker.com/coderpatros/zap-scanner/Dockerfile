FROM owasp/zap2docker-stable:2.8.0

# need to run as root to be able to write test results in Azure DevOps release pipelines :(
USER root
ENV HOME /root/
RUN mv /home/zap/.ZAP /root/.ZAP && \
    chown root:root -R /root/.ZAP

RUN apt-get update && apt-get install -q -y --fix-missing \
    libsaxonb-java && \
	apt-get clean && \
    rm -rf /var/lib/apt/lists/*

ADD https://github.com/patros/zap2junit/raw/master/zap2junit.xsl /zap2junit.xsl

# trick to use local version of zap2junit.xsl if present
COPY scan.sh zap2junit.xs[l] /
RUN chmod +x /scan.sh
COPY patch_zap_junit.py /

ENTRYPOINT [ "/scan.sh" ]
CMD [""]
