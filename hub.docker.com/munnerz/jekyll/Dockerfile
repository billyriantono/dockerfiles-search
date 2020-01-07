FROM debian

RUN apt-get update && \
	apt-get install -y ruby ruby-dev nodejs gcc git rsync make && \
	gem install jekyll && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*