FROM nixos/nix:latest
RUN nix-channel --add https://nixos.org/channels/nixpkgs-unstable nixpkgs
RUN nix-channel --update
RUN nix-env -iA nixpkgs.s-tar nixpkgs.bzip2 nixpkgs.gnutar nixpkgs.gzip nixpkgs.lzma nixpkgs.p7zip nixpkgs.pigz nixpkgs.pixz nixpkgs.unzip nixpkgs.zip 