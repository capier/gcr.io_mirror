Google Container Registry Mirror [last sync 2018-06-18 02:13 UTC]
-------

[![Sync Status](https://travis-ci.org/anjia0532/gcr.io_mirror.svg?branch=sync)](https://travis-ci.org/anjia0532/gcr.io_mirror)

Syntax
-------

```bash
gcr.io/namespace/image_name:image_tag 
#eq
anjia0532/namespace.image_name:image_tag
```

Example
-------

```bash
docker pull gcr.io/google-containers/federation-controller-manager-arm64:v1.3.1-beta.1 
# eq 
docker pull anjia0532/google-containers.federation-controller-manager-arm64:v1.3.1-beta.1
```

ReTag anjia0532 images to gcr.io 
-------

```bash
# replace gcr.io/google-containers/federation-controller-manager-arm64:v1.3.1-beta.1 to real image
# this will convert gcr.io/google-containers/federation-controller-manager-arm64:v1.3.1-beta.1 
# to anjia0532/google-containers.federation-controller-manager-arm64:v1.3.1-beta.1 and pull it

images=$(cat img.txt)
#or 
#images=$(cat <<EOF
# gcr.io/google-containers/federation-controller-manager-arm64:v1.3.1-beta.1
# gcr.io/google-containers/federation-controller-manager-arm64:v1.3.1-beta.1
# gcr.io/google-containers/federation-controller-manager-arm64:v1.3.1-beta.1
#EOF)

eval $(echo |
        sed 's/gcr\.io/anjia0532/g;s/\//\./g;s/ /\n/g;s/anjia0532\./anjia0532\//g' |
        uniq |
        awk '{print "docker pull "$1";"}'
       )

# this code will retag all of anjia0532's image from local  e.g. anjia0532/google-containers.federation-controller-manager-arm64:v1.3.1-beta.1 
# to gcr.io/google-containers/federation-controller-manager-arm64:v1.3.1-beta.1

for img in $(docker images --format "{{.Repository}}:{{.Tag}}"| grep "anjia0532"); do
  n=$(echo | awk -F'[/.:]' '{printf "gcr.io/%s/%s",$2,$3}')
  tag=$(echo | awk -F'[:]' '{printf ":%s",$2}')
  docker tag  ""
done
```

[Changelog](./CHANGES.md)
-------

Mirror 6 namespaces image from gcr.io
-----


[gcr.io/google-samples/*](./google-samples/README.md)


[gcr.io/kubernetes-helm/*](./kubernetes-helm/README.md)


[gcr.io/k8s-minikube/*](./k8s-minikube/README.md)


[gcr.io/tf-on-k8s-dogfood/*](./tf-on-k8s-dogfood/README.md)


[gcr.io/spinnaker-marketplace/*](./spinnaker-marketplace/README.md)


[gcr.io/google-containers/*](./google-containers/README.md)


