FROM ubuntu:latest
RUN apt-get update && \
	apt-get install -y curl libgtk2.0-0 libx11-xcb-dev libxtst6 libxss1 libgconf2-4 libnss3 libasound2 && \
	rm -rf /var/lib/apt/lists/*
RUN curl --fail --location --remote-name --remote-header-name "https://dl.pstmn.io/download/latest/linux64" && \
	tar -xvf *.tar.gz && \
	rm *.tar.gz
ENTRYPOINT ["/Postman/Postman"]
