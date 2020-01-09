FROM vozzy/wso2base:latest
MAINTAINER Vernon Osborne <v.osborne.dev@gmail.com>
# am version
ENV AM_VERSION=1.10.0
# download and add am
RUN \
	wget -P /opt --user-agent="testuser" --referer="http://connect.wso2.com/wso2/getform/reg/new_product_download" \
		http://product-dist.wso2.com/products/api-manager/$AM_VERSION/wso2am-$AM_VERSION.zip && \
	unzip /opt/wso2am-$AM_VERSION.zip -d /opt && \
	rm /opt/wso2am-$AM_VERSION.zip
	# expose ports (offset=o)
EXPOSE 9763 9443 8280 8243
CMD /bin/bash /opt/wso2am-$AM_VERSION/bin/wso2server.sh
