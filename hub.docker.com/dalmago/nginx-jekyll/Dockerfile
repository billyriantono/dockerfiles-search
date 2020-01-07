FROM nginx

# Install jekyll and its dependencies
RUN apt-get update && apt-get -y install ruby ruby-dev rubygems git gcc make \
	&& git clone https://github.com/rubygems/rubygems.git /home/rubygems/ \
	&& rm -rf /var/lib/apt/lists/* 

WORKDIR /home/rubygems

RUN git submodule update --init && ruby setup.rb \
	&& gem install jekyll jekyll-paginate
	
WORKDIR /home
RUN rm -rf /home/*
