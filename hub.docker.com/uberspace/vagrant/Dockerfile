FROM ruby
ENTRYPOINT ["/vagrant/exec/vagrant"]
WORKDIR /vagrant
RUN git clone https://github.com/hashicorp/vagrant.git /vagrant
RUN bundle --binstubs exec
