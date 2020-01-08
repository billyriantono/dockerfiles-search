FROM tristan957/rust:latest

RUN apt-get update; \
	apt-get install -y --no-install-recommends \
		libgtk-3-dev \
        clang-format-4.0 \
		; \
	rm -rf /var/lib/apt/lists/*;
