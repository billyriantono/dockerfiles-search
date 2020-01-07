FROM python:3.6.7

MAINTAINER john.wang <wywincl@gmail.com>

#=========================================
# Install robotframework and library.
#=========================================
RUN pip install -U robotframework==3.0.4 \
&& pip install -U robotframework-seleniumlibrary \
&& pip install --upgrade RESTinstance \
&& pip install -U requests \
&& pip install -U robotframework-requests \
&& pip install -U requests_toolbelt \
&& pip install -U robotframework-pabot \
&& pip install -U jsonschema \
&& pip install -U robotframework-lint \
&& pip install -U pyyaml \
&& pip install -U robotframework-databaselibrary

#============
# workspace
#============
RUN mkdir /etc/robot
VOLUME /etc/robot
WORKDIR /etc/robot

ENTRYPOINT ["pabot"]
