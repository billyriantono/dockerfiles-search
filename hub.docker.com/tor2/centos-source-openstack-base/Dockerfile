FROM tor2/centos-source-base:4.0.0
MAINTAINER Kolla Project (https://launchpad.net/kolla)






    

RUN yum -y install git iproute openssl && yum clean all



    
        
    

RUN yum -y install gcc gcc-c++ libffi-devel libxml2-devel libxslt-devel libyaml-devel MariaDB-devel openldap-devel openssl-devel postgresql postgresql-devel python-devel sqlite-devel zip && yum clean all


RUN curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py \
    && python get-pip.py \
    && rm get-pip.py




#ADD openstack-base-archive /openstack-base-source
RUN mkdir -p /openstack-base-source && git clone https://github.com/openstack/requirements.git -b stable/ocata
RUN ln -s openstack-base-source/* /requirements \
    && mkdir -p /var/lib/kolla \
    && pip --no-cache-dir install -U virtualenv \
    && virtualenv --system-site-packages /var/lib/kolla/venv

RUN /var/lib/kolla/venv/bin/pip --no-cache-dir install --upgrade -c requirements/upper-constraints.txt Babel Mako MarkupSafe Paste PasteDeploy PyYAML Routes SQLAlchemy Tempita WebOb alembic amqp anyjson aodhclient appdirs cachetools cliff cmd2 contextlib2 debtcollector decorator enum34 eventlet fasteners funcsigs functools32 futures futurist gnocchiclient greenlet iso8601 jinja2 jsonpatch jsonpointer jsonschema keystoneauth1 keystonemiddleware kombu monotonic msgpack-python MySQL-python netaddr netifaces os-client-config oslo.concurrency oslo.config oslo.context oslo.db oslo.i18n oslo.log oslo.messaging oslo.middleware oslo.policy oslo.serialization oslo.service oslo.utils oslo.vmware pbr pika pika-pool positional prettytable pycadf pycrypto pyinotify pymysql pyparsing python-barbicanclient python-ceilometerclient python-cinderclient python-cloudkittyclient python-congressclient python-dateutil python-designateclient python-editor python-glanceclient python-heatclient python-ironicclient python-keystoneclient python-magnumclient python-manilaclient python-memcached python-mistralclient python-muranoclient python-neutronclient python-novaclient python-openstackclient python-saharaclient python-swiftclient python-troveclient python-zaqarclient pytz repoze.lru requests requestsexceptions retrying simplejson six sqlalchemy-migrate sqlparse stevedore unicodecsv warlock wrapt 

ENV PATH /var/lib/kolla/venv/bin:$PATH



