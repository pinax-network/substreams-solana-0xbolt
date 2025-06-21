ENDPOINT ?= mainnet.sol.streamingfast.io:443

.PHONY: build
build:
	CARGO_TARGET_DIR=./target cargo build --target wasm32-unknown-unknown --release

.PHONY: stream
stream: build
	if [ -n "$(STOP)" ]; then \
		substreams gui -e $(ENDPOINT) substreams.yaml raydium_amm_events -s $(START) -t $(STOP) --limit-processed-blocks 0; \
	else \
		substreams gui -e $(ENDPOINT) substreams.yaml raydium_amm_events -s $(START) --limit-processed-blocks 0; \
	fi

.PHONY: protogen
protogen:
	substreams protogen ./substreams.yaml --exclude-paths="sf/substreams,google"

.PHONY: package
package:
	substreams pack ./substreams.yaml
