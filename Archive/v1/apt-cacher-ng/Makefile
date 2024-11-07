all: build-docker push-docker

build-docker:
	@docker build --tag=nickfedor/apt-cacher-ng:latest .

push-docker:
	@docker push nickfedor/apt-cacher-ng

build-ghcr:
	@ docker build . -t ghcr.io/nicholas-fedor/apt-cacher-ng:latest

push-ghcr:
	@ docker push ghcr.io/nicholas-fedor/apt-cacher-ng:latest