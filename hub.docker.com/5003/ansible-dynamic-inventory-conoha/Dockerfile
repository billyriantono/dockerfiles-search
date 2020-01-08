FROM 5003/builder:full
ENV ANSIBLE_HOSTS /work/hosts.py
WORKDIR /work/
RUN apk add --no-cache --virtual .builder python2-dev && \
    apk add --no-cache py2-pip \
                       py2-paramiko \
                       py2-yaml && \
    pip install python-openstackclient \
                shade \
                ansible==2.1.4.0 && \
    curl --location https://github.com/ansible/ansible/raw/c3ffe0a838cd171c8e9f20dcca96b52f9f68ed2f/contrib/inventory/openstack.py \
    | sed "s|server\['id'\]|server['metadata']['instance_name_tag']|g" > $ANSIBLE_HOSTS && \
    chmod +x $ANSIBLE_HOSTS && \
    apk del --no-cache .builder