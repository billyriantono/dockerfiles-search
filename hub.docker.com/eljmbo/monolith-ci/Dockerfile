FROM mojibakeumd/docker-rspec-puppet@sha256:3b949ce4cbc17ed86307a1dba229b07ca510f08f71449dc6bb3650c137acb8b3

RUN apt-get update

RUN apt-get install sudo openssh-client python-pip python-yaml -y

RUN pip install pyrx

RUN gem install librarian-puppet
RUN gem install puppet -v '< 5.0.0'
RUN gem install puppetlabs_spec_helper -v '0.10.3'
RUN gem install puppet-lint -v '>= 1.0.0'
RUN gem install facter -v '>= 1.7.0'
RUN gem install rspec_junit_formatter -v '0.2.3'
RUN gem install parallel_tests
