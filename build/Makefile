all: build
image=registry.bizsaas.net/devops/nacos-server:1.4.3-SNAPSHOT-security
push:
	docker buildx build --pull --platform linux/amd64,linux/arm64 -t $(image) . --push
inspect:
	docker buildx imagetools inspect $(image)
