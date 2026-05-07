.PHONY: build brewdeps

BREWFILE  := Brewfile
TIMESTAMP := .brewbundle.timestamp
BREWPRFX  := $(shell brew --prefix)
SECPK256  := Cellar/secp256k1@0.3.2/0.3.2/lib/pkgconfig
SECPKCFG  := $(BREWPRFX)/$(SECPK256)
GHC96     := Cellar/ghc@9.6/9.6.7/bin
GHCPATH   := $(BREWPRFX)/$(GHC96)

build: export PATH := $(GHCPATH):$(PATH)
build: export PKG_CONFIG_PATH := $(SECPKCFG):$(PKG_CONFIG_PATH)
build: kupo.cabal
	cabal build

kupo.cabal: brewdeps package.yaml
	hpack

brewdeps: $(TIMESTAMP)

$(TIMESTAMP): $(BREWFILE)
	brew bundle check || brew bundle install
	touch $(TIMESTAMP)

