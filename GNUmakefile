BREWFILE  := Brewfile
TIMESTAMP := .brewbundle.timestamp

SECPKPATH := $(shell brew --prefix secp256k1@0.3.2)/lib/pkgconfig
GHC96PATH := $(shell brew --prefix ghc@9.6)/bin

build: export PATH := $(GHC96PATH):$(PATH)
build: export PKG_CONFIG_PATH := $(SECPKPATH):$(PKG_CONFIG_PATH)
build: kupo.cabal
	cabal build

kupo.cabal: $(TIMESTAMP) package.yaml
	hpack

$(TIMESTAMP): $(BREWFILE)
	brew bundle check || brew bundle install
	touch $(TIMESTAMP)

