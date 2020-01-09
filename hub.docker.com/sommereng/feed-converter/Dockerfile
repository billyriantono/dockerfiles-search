FROM golang

# Update the operating system and install base tools:
RUN \
	apt-get update && \
	apt-get upgrade -y

# Install libraries:
RUN \
	go get github.com/gorilla/feeds && \
	go get github.com/mmcdole/gofeed
	
# Insert all files from the repo (from the current directory):
ADD . /go/src/github.com/SommerEngineering/FeedConverter/

# Compile and Setup
RUN	\
	cd /go/src/github.com/SommerEngineering/FeedConverter && \

	# Compile the code:
	go install && \

	# Copy the final binary to the home folder:
	cp /go/bin/FeedConverter /home && \
	chmod 0777 /home/FeedConverter && \

	# Delete the entire Go workspace:
	rm -r -f /go

# Run anything below as nobody:
USER nobody

# Provide HTTP by port 50000:
EXPOSE 50000

# Define the working directory:
WORKDIR /home

# The default command to run, if a container starts:
CMD ["./FeedConverter"]