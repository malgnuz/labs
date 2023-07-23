# Installation Procedure of SRIOV-Network-operator

## Create the namespace

`oc create -f sriov-namespace.yaml`

## Create the OperatorGroup

`oc create -f sriov-operatorgroup.yaml`

## Create the Subscription

`oc create -f sriov-subscription.yaml`
