PACKAGES := $(go list ./... | grep -v /vendor/)

# Dependencies Management
.PHONY: vendor-prepare
vendor-prepare:
	@echo "Installing glide"
	@curl https://glide.sh/get | sh

Gopkg.lock: Gopkg.toml
	@glide update

.PHONY: vendor-update
vendor-update:
	@dep ensure -update

vendor: Gopkg.lock
	@dep ensure

vendor-optimize: vendor
	@dep prune

.PHONY: clean-vendor
clean-vendor:
	@rm -rf vendor

# Linter
.PHONY: lint-prepare
lint-prepare:
	@echo "Installing gometalinter"
	@go get -u github.com/alecthomas/gometalinter
	@gometalinter --install

.PHONY: lint
lint: vendor
	@gometalinter --cyclo-over=20 --deadline=2m $(PACKAGES)

# Testing
.PHONY: test
test: vendor
	@go test $(ARG)

.PHONY: bench
bench: vendor
	@go test -bench=.

# Build and Installation
.PHONY: install
install: vendor
	@go install $(PACKAGES)
