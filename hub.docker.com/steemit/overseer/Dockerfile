FROM haskell
RUN cabal update
RUN cabal install cabal-install
RUN cabal install -j elm-compiler-0.14.1 elm-package-0.4 elm-make-0.1.1
RUN cabal install -j elm-repl-0.4 elm-reactor-0.3
