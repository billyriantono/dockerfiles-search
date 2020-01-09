FROM purmode/hubcms

MAINTAINER Purmode R <prdev@outlook.com>

ENV HUBSITE='myhubsite'

RUN touch /hub_install_script.sh \
	&& chmod +x /hub_install_script.sh \
	&& echo "#!/bin/bash" > /hub_install_script.sh \
	&& echo "service mysql start; sleep 3" >> /hub_install_script.sh \
	&& echo "service apache2 start; sleep 3" >> /hub_install_script.sh \
	&& echo "hzcms install \$HUBSITE" >> /hub_install_script.sh \
	&& echo "hzcms update" >> /hub_install_script.sh \
	&& echo "a2dissite default default-ssl" >> /hub_install_script.sh \
	&& echo "a2ensite \$HUBSITE \$HUBSITE-ssl" >> /hub_install_script.sh \
	&& echo "service apache2 restart" >> /hub_install_script.sh \
	&& echo "apt-get update" >> /hub_install_script.sh \
	&& echo "apt-get install -y hubzero-cms-2.1.0" >> /hub_install_script.sh \
	&& echo "hzcms update" >> /hub_install_script.sh \
	&& echo "apt-get purge -y hubzero-cms-2.0.0 && apt-get clean" >> /hub_install_script.sh \
	&& echo "mv /hub_install_script.sh /hub_install_tmp.sh" >> /hub_install_script.sh \
	&& echo "echo \"#!/bin/bash\" > /hub_install_tmp.sh" >> /hub_install_script.sh \
	&& echo "echo \"mv /hub_install_tmp.sh /hub_install_script.sh\" >> /hub_install_tmp.sh" >> /hub_install_script.sh \
	&& echo "echo \"echo \\\"#!/bin/bash\\\" > /hub_install_script.sh\" >> /hub_install_tmp.sh" >> /hub_install_script.sh \
	&& echo "echo \"echo \\\"service mysql start\\\" >> /hub_install_script.sh\" >> /hub_install_tmp.sh" >> /hub_install_script.sh \
	&& echo "echo \"echo \\\"service apache2 start\\\" >> /hub_install_script.sh\" >> /hub_install_tmp.sh" >> /hub_install_script.sh \
	&& echo "echo \"echo \\\"/bin/bash\\\" >> /hub_install_script.sh\" >> /hub_install_tmp.sh" >> /hub_install_script.sh \
	&& echo "echo \"sh /hub_install_script.sh\" >> /hub_install_tmp.sh" >> /hub_install_script.sh \
	&& echo "sh /hub_install_tmp.sh" >> /hub_install_script.sh

CMD ["/hub_install_script.sh"]

EXPOSE 80 443
