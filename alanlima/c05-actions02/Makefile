DOCKER_REGISTRY?=alanrlima
IMAGE_NAME?=devops-c05-actions02
COMMIT_SHA?=$(shell git rev-parse --short HEAD)

build:
	@docker build \
		-t ${DOCKER_REGISTRY}/${IMAGE_NAME}:${COMMIT_SHA}\
		-f v1.Dockerfile .
.PHONY:build

push:
	@docker push ${DOCKER_REGISTRY}/${IMAGE_NAME}:${COMMIT_SHA}
.PHONY:push

login:
	docker login \
		--username ${DOCKER_REGISTRY} \
		--password ${DOCKER_TOKEN}
.PHONY:login

get_dockerhub_url:
	@echo "https://hub.docker.com/repository/docker/${DOCKER_REGISTRY}/${IMAGE_NAME}/tags?page=1&name=${COMMIT_SHA}"
.PHONY:get_dockerhub_url

ci_github_set_outputs:
	@echo "::set-output name=url::$(shell make get_dockerhub_url)"
	@echo "::set-output name=image_name::${DOCKER_REGISTRY}/${IMAGE_NAME}:${COMMIT_SHA}"
.PHONY:ci_github_set_outputs

all: build push
.PHONY: all