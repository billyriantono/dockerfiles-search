FROM nixos/nix

ENV NIXPKGS nixos-19.09

RUN nix-channel --add https://nixos.org/channels/${NIXPKGS} nixpkgs
RUN nix-channel --update
RUN nix-env -i skopeo kubectl git
