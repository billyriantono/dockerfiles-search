FROM mojibakeumd/docker-rspec-puppet@sha256:3b949ce4cbc17ed86307a1dba229b07ca510f08f71449dc6bb3650c137acb8b3

RUN apt-get update \
	&& apt-get install software-properties-common -y \
	&& add-apt-repository 'deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main' \
	&& apt-get update \
	&& apt-get install sudo openssh-client python-dev python-pip python-yaml ansible=2.8.2-1ppa~trusty -y \
	&& rm -rf /var/lib/apt/lists/* \
	&& sed -i 's/httpredir.debian.org/aptrepo.piksel.com/g' /etc/apt/sources.list \
	&& rm -rf Python-3.7.3* /var/lib/apt/lists/* /tmp/* /var/tmp/* \
	&& apt-get clean \
    && pip install -U pip \
	&& pip install pyrx awscli ansible-lint \
    && gem install librarian-puppet puppet:4.10.12 puppetlabs_spec_helper:0.10.3 puppet-lint:2.3.6 facter:2.5.1 rspec_junit_formatter:0.2.3 parallel:1.12.1 parallel_tests:2.7.0


#RUN gem install puppet -v '< 5.0.0'
#RUN gem install puppetlabs_spec_helper -v '0.10.3'
#RUN gem install puppet-lint -v '>= 1.0.0'
#RUN gem install facter -v '>= 1.7.0'
#RUN gem install rspec_junit_formatter -v '0.2.3'
#RUN gem install parallel_tests -v '2.7.0'