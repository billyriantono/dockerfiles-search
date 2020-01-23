FROM ubuntu:12.04

ENV LC_ALL en_US.UTF-8

# install native libraries

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y language-pack-en gfortran gcc g++ make bison autoconf flex aptitude curl libcurl4-openssl-dev uuid-dev byacc python-numpy python-scipy python-netcdf python-setuptools postgresql python-setuptools python-dev libffi-dev build-essential mercurial openssh-server samba cifs-utils r-base octave gnuplot python-pip python-matplotlib git subversion libxml2-utils libx11-dev libxmu-dev libjasper-dev libxslt-dev libxml2-dev grads nco cdo mono-devel

# install python libraries

RUN easy_install -U globus-provision jsonschema lxml simplekml pykml PIL
# Install the Globus Online python nexus client
# TODO: install with package manager instead of git?
RUN git clone -b JIRA-GRAPH-1069 https://github.com/globusonline/python-nexus-client.git && cd python-nexus-client && python setup.py install && cd .. && rm -rf python-nexus-client
RUN pip install bioblend

# install galaxy

RUN mkdir galaxy
RUN mkdir galaxy/compiled_tool_dependencies

WORKDIR galaxy

RUN wget https://bitbucket.org/faceit/galaxy/get/default.tar.gz --quiet -O galaxy.tar.gz
RUN mkdir galaxy-python
RUN mkdir extract && tar xvzf galaxy.tar.gz -C extract && mv extract/$(ls extract)/* galaxy-python && rm -rf extract && rm galaxy.tar.gz

WORKDIR galaxy-python

RUN mv universe_wsgi.ini.sample universe_wsgi.ini

# download eggs
RUN python scripts/fetch_eggs.py
# create & migrate database
RUN python scripts/create_db.py

# modify configuration

COPY tool_conf.xml /galaxy/galaxy-python/tool_conf.xml

# database is SQLite by default
RUN sed -i 's|#tool_dependency_dir = None|tool_dependency_dir = /galaxy/compiled_tool_dependencies|g' universe_wsgi.ini
RUN sed -i 's|#tool_config_file|tool_config_file|g' universe_wsgi.ini
RUN sed -i 's|#tool_path|tool_path|g' universe_wsgi.ini
RUN sed -i 's|#admin_users = None|admin_users = admin@galaxy.org|g' universe_wsgi.ini
RUN sed -i 's|#master_api_key=changethis|master_api_key=HSNiugRFvgT574F43jZ7N9F3|g' universe_wsgi.ini
# Render SVG images properly
RUN sed -i 's|#serve_xss_vulnerable_mimetypes.*|serve_xss_vulnerable_mimetypes = True|g' universe_wsgi.ini
RUN sed -i 's|#host = 127.0.0.1|host = 0.0.0.0|g' universe_wsgi.ini

RUN cp tool_sheds_conf.xml.sample tool_sheds_conf.xml
RUN sed -i '/tool_shed name="Galaxy test tool shed"/i<tool_shed name="Galaxy-ES" url="http://usefaceit.org:9009/"/>' tool_sheds_conf.xml

EXPOSE 8080

VOLUME ["/galaxy/galaxy-python/database", "/galaxy/compiled_tool_dependencies"]

CMD ["./run.sh"]
