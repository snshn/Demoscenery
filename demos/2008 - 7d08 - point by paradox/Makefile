TAG = parties.2008.7d08.demo.pointbyparadox

all: build run
.PHONY: all

build:
	@podman build -t ${TAG} .
.PHONY: build

run:
	@podman run -p 10000:10000 ${TAG}
.PHONY: run

clean:
	@podman rmi $(podman images | grep "${TAG}" | awk '{print $"3"}') --force
.PHONY: clean
