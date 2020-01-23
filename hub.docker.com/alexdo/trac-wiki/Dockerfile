FROM alexdo/trac-base:latest

RUN easy_install \
	https://trac-hacks.org/svn/markdownmacro/trunk \
	https://trac-hacks.org/svn/tocmacro/0.11 \
	https://trac-hacks.org/svn/autocompleteusersplugin/trunk \
	https://trac-hacks.org/svn/awesomeattachmentsplugin/trunk \
	https://trac-hacks.org/svn/basicthemeeditorplugin/trunk \
	https://trac-hacks.org/svn/siteuploadplugin/trunk \
	https://trac-hacks.org/svn/accountmanagerplugin/tags/acct_mgr-0.5.0 \
	https://trac-hacks.org/svn/announcerplugin/trunk \
	https://trac-hacks.org/svn/hackergotchiplugin/0.11 \
	https://trac-hacks.org/svn/tagsplugin/trunk \
	https://trac-hacks.org/svn/tractimedeltaupdatorplugin/0.12

RUN pip install trac-emoji

RUN apt-get update -qq \
	&& apt-get install -y -qq libldap2-dev libsasl2-dev libssl-dev \
	&& rm -r /var/lib/apt/lists /var/cache/apt/archives \
	&& pip install python-ldap \
	&& easy_install https://trac-hacks.org/svn/ldapauthnzplugin/trunk


EXPOSE 3000

ENTRYPOINT ["tracd"]
CMD ["-p", "3000", "-e", "/trac"]