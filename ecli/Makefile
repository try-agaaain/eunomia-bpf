LIBEUNOMIA := ../bpf-loader/build/lib/Release/libeunomia.a
LIBWASM_BPF := ../wasm-runtime/build/libwasm-bpf_LIB.a

.PHONY: build
build: $(LIBEUNOMIA) $(LIBWASM_BPF)
	echo "my info: begin cargo build"
	cargo build --release -v

$(LIBEUNOMIA):
	$(MAKE) -C ../bpf-loader install
	echo "my info: bpf-loader install is done"

$(LIBWASM_BPF):
	mkdir -p ../wasm-runtime/include/wasm-bpf
	$(MAKE) -C ../wasm-runtime build-cpp
	echo "my info: wasm-bpf install is done"

install: $(LIBEUNOMIA) $(LIBWASM_BPF)## install the package to the `INSTALL_LOCATION`
	mkdir -p ../wasm-runtime/include/wasm-bpf
	rm -rf target/
	echo "my info: begin cargo build"
	cargo build --release -v
	mkdir -p ~/.eunomia/bin
	cp ./target/release/ecli ~/.eunomia/bin/ecli

install-deps:
	sudo apt install libssl-dev
	sudo apt install pkg-config
