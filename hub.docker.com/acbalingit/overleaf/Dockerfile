# --------------------------------------------------
# Overleaf Base Image (sharelatex/sharelatex-base)
# --------------------------------------------------

FROM phusion/baseimage:0.11

ENV baseDir .


# Install dependencies
# --------------------
RUN apt-get update
RUN apt-get install -y sudo
RUN apt-get install -y build-essential wget net-tools unzip time imagemagick optipng strace nginx git python zlib1g-dev libpcre3-dev aspell aspell-en aspell-af aspell-am aspell-ar aspell-ar-large aspell-bg aspell-bn aspell-br aspell-ca aspell-cs aspell-cy aspell-da aspell-de aspell-el aspell-eo aspell-es aspell-et aspell-eu-es aspell-fa aspell-fo aspell-fr aspell-ga aspell-gl-minimos aspell-gu aspell-he aspell-hi aspell-hr aspell-hsb aspell-hu aspell-hy aspell-id aspell-is aspell-it aspell-kk aspell-kn aspell-ku aspell-lt aspell-lv aspell-ml aspell-mr aspell-nl aspell-nr aspell-ns  aspell-pa aspell-pl aspell-pt aspell-pt-br aspell-ro aspell-ru aspell-sk aspell-sl aspell-ss aspell-st aspell-sv aspell-tl aspell-tn aspell-ts aspell-uk aspell-uz aspell-xh aspell-zu


# Install qpdf
# ------------
WORKDIR /opt
RUN wget https://s3.amazonaws.com/sharelatex-random-files/qpdf-6.0.0.tar.gz && tar xzf qpdf-6.0.0.tar.gz
WORKDIR /opt/qpdf-6.0.0
RUN ./configure && make && make install && ldconfig


# Install Node
# ------------
RUN curl -sL https://deb.nodesource.com/setup_10.x | sudo bash -
RUN apt-get install -y nodejs
RUN npm install -g grunt-cli


# Install Node6 (required by some services)
# -----------------------------------------
RUN wget https://nodejs.org/dist/v6.17.1/node-v6.17.1-linux-x64.tar.gz && \
	mkdir -p /opt/nodejs && tar -xzf node-v6.17.1-linux-x64.tar.gz -C /opt/nodejs/ && \
    cd /opt/nodejs && mv node-v6.17.1-linux-x64 6.17.1 && \
    ln -s /opt/nodejs/6.17.1/bin/node /usr/bin/node6


# Install TexLive
# ---------------
RUN wget http://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz && \
	mkdir /install-tl-unx && \
	tar -xvf install-tl-unx.tar.gz -C /install-tl-unx --strip-components=1
RUN echo "selected_scheme scheme-full" >> /install-tl-unx/texlive.profile && \
	/install-tl-unx/install-tl -profile /install-tl-unx/texlive.profile

# CTAN mirrors occasionally fail, in that case install TexLive against an
# specific server, for example http://ctan.crest.fr
# RUN wget http://ctan.crest.fr/tex-archive/systems/texlive/tlnet/install-tl-unx.tar.gz && \
# 	  mkdir /install-tl-unx && \
# 	  tar -xvf install-tl-unx.tar.gz -C /install-tl-unx --strip-components=1
# RUN echo "selected_scheme scheme-basic" >> /install-tl-unx/texlive.profile && \
# 	  /install-tl-unx/install-tl -profile /install-tl-unx/texlive.profile  \
# 	  -repository  http://ctan.crest.fr/tex-archive/systems/texlive/tlnet/

RUN rm -r /install-tl-unx; \
	rm install-tl-unx.tar.gz
ENV PATH /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/local/texlive/2019/bin/x86_64-linux/
RUN tlmgr install latexmk
RUN tlmgr install texcount


# Set up sharelatex user and home directory
# -----------------------------------------
RUN adduser --system --group --home /var/www/sharelatex --no-create-home sharelatex && \
	mkdir -p /var/lib/sharelatex && \
	chown www-data:www-data /var/lib/sharelatex && \
	mkdir -p /var/log/sharelatex && \
	chown www-data:www-data /var/log/sharelatex && \
	mkdir -p /var/lib/sharelatex/data/template_files && \
	chown www-data:www-data /var/lib/sharelatex/data/template_files


# Install app settings files
# --------------------------
ADD ${baseDir}/settings.coffee /etc/sharelatex/settings.coffee
ENV SHARELATEX_CONFIG /etc/sharelatex/settings.coffee


# Checkout Overleaf Community Edition repo
# ----------------------------------------
RUN git clone https://github.com/overleaf/overleaf.git \
	--depth 1 /var/www/sharelatex


# Install dependencies needed to run configuration scripts
# --------------------------------------------------------
ADD ${baseDir}/package.json /var/www/package.json
ADD ${baseDir}/git-revision.js /var/www/git-revision.js
RUN cd /var/www && npm install


# Replace overleaf/config/services.js with the list of available 
# services in Overleaf Community Edition
# --------------------------------------------------------------
ADD ${baseDir}/services.js /var/www/sharelatex/config/services.js


# Checkout services
# -----------------
RUN cd /var/www/sharelatex && \
	npm install && grunt install;


# install and compile services
# ----------------------------
RUN bash -c 'cd /var/www/sharelatex && source ./bin/install-services'
RUN bash -c 'cd /var/www/sharelatex && source ./bin/compile-services'


# Change application ownership to www-data
# ----------------------------------------
RUN	chown -R www-data:www-data /var/www/sharelatex;


# Copy runit service startup scripts to its location
# --------------------------------------------------
ADD ${baseDir}/runit /etc/service


# Configure nginx
# ---------------
RUN rm /etc/nginx/sites-enabled/default
ADD ${baseDir}/nginx/nginx.conf /etc/nginx/nginx.conf
ADD ${baseDir}/nginx/sharelatex.conf /etc/nginx/sites-enabled/sharelatex.conf


# Configure log rotation
# ----------------------
ADD ${baseDir}/logrotate/sharelatex /etc/logrotate.d/sharelatex


# Copy Phusion Image startup scripts to its location
# --------------------------------------------------
COPY ${baseDir}/init_scripts/ /etc/my_init.d/


# Stores the version installed for each service
# ---------------------------------------------
RUN cd /var/www && node git-revision > revisions.txt


EXPOSE 80

WORKDIR /

ENTRYPOINT ["/sbin/my_init"]

