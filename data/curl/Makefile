REPO:=git.kura.gg/kura/forgejo/curl
TAG:=latest
CONTAINERFILE?=Containerfile

build:
	docker buildx build --progress=plain -t $(REPO):$(TAG) --platform linux/amd64,linux/aarch64 --push -f Containerfile .

prune:
	docker buildx prune

update:
	./update-versions $(CONTAINERFILE)
