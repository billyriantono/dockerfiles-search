FROM davvdg/openstack_cli
RUN 	apt-get update -qq &&\
	apt-get install -y -q software-properties-common &&\
	apt-add-repository -y ppa:ansible/ansible &&\
	apt-get update -qq &&\
	apt-get install -y -q ansible wget vim
RUN pip install shade
RUN wget https://raw.githubusercontent.com/ansible/ansible/devel/contrib/inventory/openstack.py &&\
	mv /etc/ansible/hosts /etc/ansible/hosts.conf &&\
	mkdir /etc/ansible/hosts &&\
	mv /etc/ansible/hosts.conf /etc/ansible/hosts/ &&\
	mv openstack.py /etc/ansible/hosts/ && chmod +x /etc/ansible/hosts/openstack.py

