FROM mysql:5.7
LABEL maintainer="theokleintw@gmail.com"
WORKDIR /docker-entrypoint-initdb.d
RUN apt-get update && \
		apt-get install git -y && \
		rm -rf /var/lib/apt/lists/* && \
		git clone https://github.com/datacharmer/test_db.git /docker-entrypoint-initdb.d
