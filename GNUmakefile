.PHONY: build test

BREWFILE   := Brewfile
TIMESTAMP  := .brewbundle.timestamp
BREWPREFIX := $(shell brew --prefix)
BREWLIBS   := $(BREWPREFIX)/lib
GHC96PATH  := $(BREWPREFIX)/opt/ghc@9.6/bin

export PATH            := $(GHC96PATH):$(PATH)
export LD_LIBRARY_PATH := $(BREWLIBS):$(LD_LIBRARY_PATH)

build: kupo.cabal
	cabal build

test: kupo.cabal
	cabal test

kupo.cabal: $(TIMESTAMP) package.yaml
	hpack

$(TIMESTAMP): $(BREWFILE)
	brew bundle check || brew bundle install
	touch $(TIMESTAMP)

