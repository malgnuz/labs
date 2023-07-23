## Installation procedure of Director Operator

1. Create the **openstack** namespace

```
oc new-project openstack
```

2. Get the **osp-director-operator-bundle** from the [Red Hat Container Catalog](https://catalog.redhat.com/software/containers/search)

3. [Download](https://console.redhat.com/openshift/downloads) the **opm** tool.

4. Login at the source and destination registries:

```
podman login registry.redhat.io
podman login quay.io/maugarci
```

5. Create an index image:

```
TAG="1.3.0-11"
BUNDLE_IMG="registry.redhat.io/rhosp-rhel8/osp-director-operator-bundle:${TAG}"
INDEX_IMG="quay.io/maugarci/osp-director-operator-index:${TAG}"
opm index add --bundles ${BUNDLE_IMG} --tag ${INDEX_IMG} -u podman --pull-tool podman
```

5. Push the index image to a Registry:

```
podman push ${INDEX_IMG}
```

#PENDING#
