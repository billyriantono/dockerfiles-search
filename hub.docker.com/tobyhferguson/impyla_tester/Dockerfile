FROM centos:latest
RUN yum -y update && \
    yum -y install \
    	   cyrus-sasl-devel.x86_64\
	   cyrus-sasl-gs2.x86_64    \
	   cyrus-sasl-gssapi.x86_64 \
	   cyrus-sasl-ldap.x86_64   \
	   cyrus-sasl-lib.x86_64    \
	   cyrus-sasl-md5.x86_64    \
	   cyrus-sasl-ntlm.x86_64   \
	   cyrus-sasl-plain.x86_64  \
	   cyrus-sasl-scram.x86_64  \
	   cyrus-sasl-sql.x86_64    \
	   cyrus-sasl.x86_64        \
	   gcc \
	   gcc-c++ \
	   python-devel.x86_64 \
	   python-saslwrapper.x86_64\
	   ruby-saslwrapper.x86_64  \
	   saslwrapper-devel.x86_64 \
	   saslwrapper.x86_64  \
	   wget

RUN wget https://bootstrap.pypa.io/get-pip.py

RUN python get-pip.py

RUN pip install \
    	'setuptools>=3.4.4' \
	impyla  \
	six \
	bit_array \
	'thrift<=0.9.3' \
	pandas \
	sasl \
	'thrift_sasl==0.2.1'

COPY impyla.py .

ENTRYPOINT ["/impyla.py"]

CMD [""]



