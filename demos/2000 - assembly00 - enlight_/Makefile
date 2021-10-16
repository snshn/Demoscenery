TAG = parties.2000.assembly.demo.enlight

all: build run
.PHONY: all

build:
	@podman build -t ${TAG} .
.PHONY: build

run:
	@podman run -p 10000:10000 ${TAG}
.PHONY: run

clean:
	@echo TODO
.PHONY: clean
