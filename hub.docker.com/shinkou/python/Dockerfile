FROM python:3-stretch
RUN set -x \
	&& apt-get update \
	&& apt-get upgrade -y \
	&& apt-get install -y libsasl2-dev libsasl2-modules \
	&& apt-get clean -y
RUN pip install boto3 ec2util elasticsearch kafka-python PyHive pytz request sasl sqlalchemy thrift thrift_sasl vertica-python
