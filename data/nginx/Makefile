REPO:=git.kura.gg/kura/forgejo/nginx
TAG:=latest
CONTAINERFILE?=Containerfile

.PHONY: build
build:
	docker buildx build --progress=plain -t $(REPO):$(TAG) --platform linux/amd64,linux/aarch64 --push -f Containerfile .

.PHONY: prune
prune:
	docker buildx prune -f

.PHONY: update
update:
	bash $(PWD)/update-versions $(CONTAINERFILE)
