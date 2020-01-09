FROM frolvlad/alpine-mono:latest

RUN apk --no-cache add ca-certificates wget openssl \
    && update-ca-certificates

# Download and extract WG++ to correct paths
RUN mkdir wg++ config data && \
    wget -O /tmp/wg++.tar.gz http://webgrabplus.com/sites/default/files/download/SW/V2.1.0/WebGrabPlus_V2.1_install.tar.gz && \
    tar -zxvf /tmp/wg++.tar.gz -C /wg++/ && \
    rm /tmp/wg++.tar.gz && \
    mv /wg++/.wg++/* /wg++/ && \
    cp /wg++/bin/WebGrab+Plus.exe /wg++/bin/xmltv.dll /wg++/ && \
		cp /wg++/mdb/mdb.config.example.xml /config/mdb.config.xml && \
		cp /wg++/rex/rex.config.example.xml /config/rex.config.xml && \
		rm -rf /wg++/siteini.pack.update /wg++/doc

# Add config files
ADD WebGrab++.config.xml uk-sky.com.ini canalsat.fr.ini bein.net.ini nowtv.now.com.ini tvhebdo.com.ini tvhebdo.com.cookies.txt telerama.fr.api.ini telerama-sha1.sh /config/

RUN chmod -R +x /wg++/

CMD ["mono", "/wg++/WebGrab+Plus.exe", "/config"]
