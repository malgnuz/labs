# Installation Procedure of Kubernetes-NMState

## Create the namespace

`oc create -f nmstate-namespace.yaml`

## Create the OperatorGroup

`oc create -f nmstate-operatorgroup.yaml`

## Create the Subscription

`oc create -f nmstate-subscription.yaml`

## Create an instance of Hyperconverged 

`oc create -f nmstate-instance.ymal`
