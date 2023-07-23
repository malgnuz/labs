## Installation procedure of Director Operator

1. Create the **openstack** namespace

```
oc new-project openstack
```

2. Get the **osp-director-operator-bundle** from the [Red Hat Container Catalog](https://catalog.redhat.com/software/containers/search)

3. (Download)[https://console.redhat.com/openshift/downloads] the **opm** tool.

4. Create an index image:

```
BUNDLE_IMG="registry.redhat.io/rhosp-rhel8/osp-director-operator-bundle@sha256:c19099ac3340d364307a43e0ae2be949a588fefe8fcb17663049342e7587f055"
INDEX_IMG="quay.io/<account>/osp-director-operator-index:x.y.z-a"
opm index add --bundles ${BUNDLE_IMG} --tag ${INDEX_IMG} -u podman --pull-tool podman
```

5. Push the index image to a Registry:

```
podman push ${INDEX_IMG}
```

#PENDING#
