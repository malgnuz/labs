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

6. Create a secret to authenticate OpenShift against Quay

6.1 Copy the authentication file into a new file:

```
cp /var/run/containers/0/auth.json .auth.json
```

6.2 Create the secret object into **openstack** namespace:

```
oc create secret \
generic secret-registry \
-n openstack \
--from-file=.dockerconfigjson=.auth.json \
--type=kubernetes.io/dockerconfigjson
```

7. Create the [CatalogSource](director-catalogsource.yaml) from the Index image:

```
oc create -f director-catalogsource.yaml
```

8. Create the [OperatorGroup](director-operatorgroup.yaml):  

```
oc create -f director-operatorgroup.yaml
```

9. Create the [Subscription](director-subscription.yaml):

```
oc create -f director-subscription.yaml
```

10. Verify the Operators installed into **openstack** namespace:

```
oc get operators
NAME                                                      AGE
kubernetes-nmstate-operator.openshift-nmstate             27h
kubevirt-hyperconverged.openshift-cnv                     27h
osp-director-operator.openstack                           6m6s
sriov-network-operator.openshift-sriov-network-operator   58m
```
