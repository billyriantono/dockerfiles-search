FROM tsweb/ffmpeg
MAINTAINER Kazuhisa Kumagai <k-kumagai@ts.tv-osaka.co.jp>

#--------------------------------------
# install Ruby
#--------------------------------------

# install ruby
RUN (\
	cd /usr/local/src;\
	wget -O ruby-2.1.2.tar.gz http://cache.ruby-lang.org/pub/ruby/2.1/ruby-2.1.2.tar.gz;\
	tar zxvf ruby-2.1.2.tar.gz;\
	cd ruby-2.1.2;\
	./configure;\
	make;\
	make install;\
)

# install bundler
RUN gem install bundler

# deploy app
RUN git clone https://bitbucket.org/tvoweb2/video_storage.git /opt/video_storage
RUN git clone https://bitbucket.org/tvoweb2/yotta-framework.git /opt/video_storage/lib/yotta

RUN chmod 701 /opt/video_storage/http/start.rb
RUN chmod 701 /opt/video_storage/http/featurephone/*.rb

# install depended gems
RUN (\
	cd /opt/video_storage;\
	bundle install;\
	cd /opt/video_storage/lib/yotta;\
	bundle install;\
	cd /opt/video_storage/lib/video_storage;\
	bundle install;\
)

#--------------------------------------
# initialize
#--------------------------------------

ADD supervisor.conf /etc/supervisord/conf/service.conf
CMD ["/usr/bin/supervisord"]
