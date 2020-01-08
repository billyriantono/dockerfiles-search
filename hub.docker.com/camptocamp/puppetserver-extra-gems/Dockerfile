FROM puppet/puppetserver as installer
RUN puppetserver gem install ruby_gpg
RUN chown -R puppet:puppet /opt/puppetlabs/server/data/puppetserver/

FROM busybox
COPY --from=installer /opt/puppetlabs/server/data/puppetserver/jruby-gems/ /opt/puppetlabs/server/data/puppetserver/jruby-gems/
VOLUME /opt/puppetlabs/server/data/puppetserver/jruby-gems/
ENTRYPOINT ["/bin/true"]
