FROM rust:1.26

# Create 'app' user.
RUN groupadd --gid 1000 app \
	 && useradd --uid 1000 --gid app --shell /bin/bash --create-home app \
	 && chown -R app:app /home/app

# Install dependencies.
RUN apt-get update \
	 && apt-get install -y --no-install-recommends \
		  ca-certificates \
		  curl \
		  fish \
		  git \
		  neovim \
	 && rm -rf /var/lib/apt/lists/*

USER app
ENV USER app

# Configure fish.
ADD config.fish /home/app/.config/fish/config.fish

# Configure neovim.
ADD init.vim /home/app/.config/nvim/init.vim
RUN curl -fLo /home/app/.local/share/nvim/site/autoload/plug.vim \
		  --create-dirs \
		  https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim \
	 && nvim +PlugInstall +qall

# Create and set working space.
USER root
RUN cd /home/app \
	 && cargo new --bin --name=app src \
	 && chown -R app:app /home/app
WORKDIR /home/app/src
USER app

CMD ["nvim"]

