# bsidespdx2018 is the organization on dockerhub
REGISTRY := bsidespdx2018
DOCKER_IMAGE := pwn200

CONTAINER_TAG := ${REGISTRY}/${DOCKER_IMAGE}

target: container push deploy serve

clean: deleteDocker deleteKube
	make -C ../src clean

# Docker Configurations

container:
	make -C ../src
	docker build --no-cache --tag ${CONTAINER_TAG} ../src

push: 
	docker push ${CONTAINER_TAG}

# Kubernetes

deploy:
	cat cloud/deploy.yaml | kubectl create --namespace bsidespdxctf  -f -

serve:
	kubectl create --namespace bsidespdxctf -f cloud/service.yaml

deleteKube:
	cat cloud/deploy.yaml | kubectl delete --namespace bsidespdxctf -f -
	kubectl delete --namespace  bsidespdxctf -f cloud/service.yaml
