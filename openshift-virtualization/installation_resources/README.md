# Installation Procedure of OCP-V

## Create the namespace

`oc create -f ocpv-namespace.yaml`

## Create the OperatorGroup

`oc create -f ocpv-operatorgroup.yaml`

## Create the Subscription

`oc create -f ocpv-subscription.yaml`

NOTE: According to the documentation the apiVersion is **operators.coreos.com/v1beta1**. However it only works with **apiVersion=operators.coreos.com/v1alpha1**.

## Create an instance of Hyperconverged 

`oc create -f hco.ymal`
