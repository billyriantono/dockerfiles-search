FROM debian:9

ENV MCOLLECTIVE_IDENTITY=gitlab-ci
COPY hiera /tmp

RUN apt-get update -yqq \
 && apt-get install curl ca-certificates -yqq --no-install-recommends \
 && curl -JLO https://apt.puppet.com/puppet6-release-stretch.deb \
 && dpkg -i puppet6-release-stretch.deb \
 && rm puppet6-release-stretch.deb \
 && apt-get update -yqq \
 && apt-get install puppet-agent -yqq \
 && /opt/puppetlabs/bin/puppet module install choria-choria --target-dir=/tmp/modules \
 && /opt/puppetlabs/bin/puppet module install choria-mcollective_agent_bolt_tasks --target-dir=/tmp/modules \
 && /opt/puppetlabs/bin/puppet apply --hiera_config=/tmp/hiera/hiera.yaml --modulepath=/tmp/modules -e 'include mcollective' \
 && cp -r /tmp/modules/mcollective_choria/files/mcollective/* /opt/puppetlabs/mcollective/plugins/mcollective/ \
 && cp -r /tmp/modules/mcollective_agent_*/files/mcollective/* /opt/puppetlabs/mcollective/plugins/mcollective/ \
 && echo 'bWlkZGxld2FyZV9ob3N0cyA9IEBOQVRTQApwdXBwZXRjYV9ob3N0ID0gQFBVUFBFVENBQApwdXBwZXRjYV9wb3J0ID0gODE0MApwdXBwZXRkYl9ob3N0ID0gQFBVUFBFVERCQApwdXBwZXRkYl9wb3J0ID0gODA4MQpwdXBwZXRzZXJ2ZXJfaG9zdCA9IEBQVVBQRVRTRVJWRVJACnB1cHBldHNlcnZlcl9wb3J0ID0gODE0MAo=' | base64 -d > /etc/puppetlabs/mcollective/plugin.d/choria.cfg \
 && apt-get remove curl ca-certificates -yqq \
 && apt-get autoremove -yqq \
 && apt-get clean \
 && rm -rf /tmp/hiera /tmp/modules /var/lib/apt/lists/* \
 && adduser --disabled-password --gecos '' $MCOLLECTIVE_IDENTITY \
 && chown -R $MCOLLECTIVE_IDENTITY /etc/puppetlabs/mcollective

COPY setup-mco.sh /usr/local/bin/setup-mco
COPY entrypoint.sh /usr/local/bin/entrypoint

USER $MCOLLECTIVE_IDENTITY
WORKDIR /home/$MCOLLECTIVE_IDENTITY
ENTRYPOINT ["/usr/local/bin/entrypoint"]
