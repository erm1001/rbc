PKG=camweather
PkgVersion=$(shell grep Version $(PKG)/DESCRIPTION | sed -e 's/Version: //')
PKGTGZ=$(PKG)_$(PkgVersion).tar.gz

setvars:
ifeq (${R_HOME},)
R_HOME= $(shell R RHOME)
endif

build: 
	"$(R_HOME)/bin/R" CMD build $(PKG)

check: 
	"$(R_HOME)/bin/R" CMD check $(PKGTGZ)

install: 
	"$(R_HOME)/bin/R" CMD INSTALL $(PKGTGZ)

roxygen:
	"$(R_HOME)/bin/R" --vanilla -e "library(roxygen2); roxygenize('"$(PKG)"', roclets=\"rd\")";

all:
	make roxygen
	make build
	make check
	make install

.PHONY: build check install roxygen
