# Extra package for projects that need `wkhtmltopdf` as well.
# TO build: docker build -t edoburu/python-runner:wkhtmltopdf .
FROM edoburu/python-runner:base
RUN apt-get update && \
	apt-get install -y xz-utils libxext6 fontconfig libxrender1 && \
	python -c 'import urllib; urllib.urlretrieve("https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.4/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz", "wkhtmltox.tar.xz")' && \
	tar --directory=/usr/local --strip 1 -xJf wkhtmltox.tar.xz && \
	apt-get clean && rm -rf /var/lib/apt/lists/* /var/cache/debconf/*-old
