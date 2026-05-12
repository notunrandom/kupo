.PHONY: build dependencies test

BREWFILE   := Brewfile
TIMESTAMP  := .brewbundle.timestamp
BREWPREFIX := $(shell brew --prefix)
BREWLIBS   := $(BREWPREFIX)/lib
GHC96PATH  := $(BREWPREFIX)/opt/ghc@9.6/bin
SECPLIBS   := $(BREWPREFIX)/opt/secp256k1@0.3.2/lib
SECPKGCONF := $(SECPLIBS)/pkgconfig

export PATH            := $(GHC96PATH):$(PATH)
export PKG_CONFIG_PATH := $(SECPKGCONF):$(PKG_CONFIG_PATH)
export LD_LIBRARY_PATH := $(SECPLIBS):$(BREWLIBS):$(LD_LIBRARY_PATH)

dependencies: kupo.cabal
	cabal build --only-dependencies

build: kupo.cabal
	cabal build

test: kupo.cabal
	cabal test

kupo.cabal: $(TIMESTAMP) package.yaml
	hpack
	cabal update

$(TIMESTAMP): $(BREWFILE)
	brew bundle check || brew bundle install
	touch $(TIMESTAMP)

