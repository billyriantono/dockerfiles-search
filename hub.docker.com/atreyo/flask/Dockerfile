FROM python:3.6.5-jessie

ENV PATH /usr/local/bin:$PATH

ENV LANG C.UTF-8

ENV PYTHON_PIP_VERSION 9.0.1

RUN set -ex; \
	\
	wget -O get-pip.py 'https://bootstrap.pypa.io/get-pip.py'; \
	\
	python get-pip.py \
		--disable-pip-version-check \
		--no-cache-dir \
		"pip==$PYTHON_PIP_VERSION" \
	; \
	pip --version; \
	\
	find /usr/local -depth \
		\( \
			\( -type d -a \( -name test -o -name tests \) \) \
			-o \
			\( -type f -a \( -name '*.pyc' -o -name '*.pyo' \) \) \
		\) -exec rm -rf '{}' +; \
	rm -f get-pip.py
RUN pip install --upgrade pip
RUN pip install elasticsearch flask flask_debugtoolbar flask-bootstrap

#COPY site/ /usr/src/app/

WORKDIR /usr/src/app/

EXPOSE 5000

ENTRYPOINT ["python3", "-m", "flask", "run", "--host=0.0.0.0"]
#CMD ["python3"]
