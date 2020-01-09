FROM stlhrt/consul-template

RUN echo 'deb http://ppa.launchpad.net/vbernat/haproxy-1.5/ubuntu trusty main' >> /etc/apt/sources.list && \
    echo 'deb-src http://ppa.launchpad.net/vbernat/haproxy-1.5/ubuntu trusty main' >> /etc/apt/sources.list && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 505D97A41C61B9CD && \
    apt-get update && \
    apt-get install -y --no-install-recommends haproxy && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

ADD config.hcl /opt/template/config.hcl
ADD haproxy.ctmpl /opt/template/haproxy.ctmpl
ADD hap.sh /opt/haproxy/hap.sh
RUN chmod +x /opt/haproxy/hap.sh
ADD 55-haproxy.json /opt/consul/conf/55-haproxy.json

RUN mkdir -p /opt/haproxy/logs
