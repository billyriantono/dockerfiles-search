FROM nixos/nix:2.0.4

MAINTAINER Jordan Cran jordan@instantepiphany.com.au

RUN wget https://github.com/barnybug/s3/releases/download/1.1.4/s3-linux-amd64 \
  && mv s3-linux-amd64 s3 && chmod +x s3 && mv s3 /usr/local/bin/s3

RUN nix-channel --add https://nixos.org/channels/nixos-18.03 nixpkgs
RUN nix-channel --add https://nixos.org/channels/nixpkgs-unstable nixpkgs-unstable
RUN nix-channel --update

RUN nix-env -iA nixpkgs-unstable.yarn
RUN nix-env -iA nixpkgs.wget
RUN nix-env -iA nixpkgs.nodejs-8_x
RUN nix-env -iA nixpkgs.git

CMD [ "/bin/bash" ]
