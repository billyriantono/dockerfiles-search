FROM vozzy/wso2base:latest
MAINTAINER Vernon Osborne <v.osborne.dev@gmail.com>
# esb version
ENV ESB_VERSION=4.9.0
# download and add esb
RUN \
	wget -P /opt --user-agent="testuser" --referer="http://connect.wso2.com/wso2/getform/reg/new_product_download" \
		http://product-dist.wso2.com/products/enterprise-service-bus/$ESB_VERSION/wso2esb-$ESB_VERSION.zip && \
	unzip /opt/wso2esb-$ESB_VERSION.zip -d /opt && \
	rm /opt/wso2esb-$ESB_VERSION.zip
# expose ports (offset=o)
EXPOSE 9763 9443 8280 8243
CMD /bin/bash /opt/wso2esb-$ESB_VERSION/bin/wso2server.sh
