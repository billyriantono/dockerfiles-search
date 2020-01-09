FROM haskellguide/nix

LABEL "maintainer"="Geoffrey Huntley <ghuntley@ghuntley.com>"
LABEL "repository"="https://github.com/haskellguide/docker-templates"
#LABEL "version"="1.0.0"

#RUN nix-channel --add https://nixos.org/channels/nixpkgs-unstable nixpkgs
RUN nix-channel --update

# base image
RUN nix-env -iA \
    nixpkgs.curl \
    nixpkgs.emacs \
    nixpkgs.git \
    nixpkgs.vim \
    nixpkgs.tmux \
    nixpkgs.wget 

# trust/use these 3rd party caches
RUN nix-env -iA cachix -f https://github.com/NixOS/nixpkgs/tarball/889c72032f8595fcd7542c6032c208f6b8033db6
RUN cachix -v use hie-nix

# haskell ide engine
RUN nix-env -iA hie84 -f https://github.com/domenkozar/hie-nix/tarball/master

# haskell
RUN nix-env -iA \
   nixpkgs.haskell.compiler.ghc844 \
   nixpkgs.haskellPackages.ghcid \
   nixpkgs.haskellPackages.hasktags \
   nixpkgs.haskellPackages.hlint \
   nixpkgs.haskellPackages.hoogle \
   nixpkgs.haskellPackages.pointfree \
   nixpkgs.haskellPackages.pointful
