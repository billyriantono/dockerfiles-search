FROM nixos/nix
RUN apk update && apk add git && \
    git clone https://github.com/gibiansky/IHaskell.git && \
    cd IHaskell && \
    nix-build release.nix --arg packages "haskellPackages: [ haskellPackages.lens ]"
RUN echo "jupyter:x:1000:1000::/home/jupyter:/bin/sh" >> /etc/passwd && \
    mkdir -p /home/jupyter/.jupyter && \
    echo '{"NotebookApp": {"password": "sha1:7ea52196911d:c32f0ee2d7799db80bf5684b47dac93a7e697371"}}' > /home/jupyter/.jupyter/jupyter_notebook_config.json && \
    chown -R jupyter /home/jupyter
USER jupyter
WORKDIR /home/jupyter
CMD /IHaskell/result/bin/ihaskell-notebook --ip 0.0.0.0 --port 8888 