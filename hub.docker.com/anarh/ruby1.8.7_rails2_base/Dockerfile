FROM anarh/ruby1.8.7_base

ADD launch_rails2_server.sh /src/scripts/launch_rails2_server.sh
RUN sudo chown railsapp /src/scripts/launch_rails2_server.sh
RUN sudo chmod +x /src/scripts/launch_rails2_server.sh

ENTRYPOINT ["/bin/bash", "-l", "-c"]
CMD ["/src/scripts/launch_rails2_server.sh"]

EXPOSE 3000
