---
linkTitle: Licensing
---

# Licensing

A newly installed Ondat cluster doesn't include a default licence. The cluster
will run unlicenced for 24 hours without any limitations. After this time
period, any new operations (for example: volume provisioning, adding nodes,
etc.) will not be possible. Note that any existing configuration, volumes and
data accessed and generated by your workload during the 24 hours or a licenced
cluster will not be impacted in the event of reaching either an unlicenced or
expired licence scenario. Normal functioning of the cluster can be unlocked by
applying a valid licence, either Personal or Commercial.

## Personal Licence

The personal licence requires the user to register and issue a licence through
Ondat.

The personal licence is free and grants a licence for a three-node Ondat
cluster with 1TiB of provisioned capacity. It is designed to enable basic
cloud-native workflows in Kubernetes that require the persistence of stateful
application data. Dynamic provisioning, distributed access to data and high
availability of volumes through synchronous replication and automatic failover
are some of the features that are available under the personal licence.

## Commercial Licence

For more information on our commercial offerings, including support, please
contact getstarted@ondat.io.

## Capacity limits

Ondat offerings might have defined capacity limits. Ondat allows provisioning
volumes until the limit of the licence is reached. Only the size of the volume
requested by the Persistent Volume Claim counts for the licence limit (whether
the volume has replication enabled or not doesn't matter).

Once the licence limit is reached, new volumes are not able to provision unless
provisioned capacity is released, i.e deleting volumes. That behaviour is not
tied to the capacity of the backend disks on your nodes.

# Obtaining a Licence

Once an Ondat cluster is deployed, either for testing purposes or in a
production environment, a Personal or Commercial licence can be issued. The one
common requirement to issue a licence is to provide the Ondat Customer Success
team with the Ondat Cluster ID. The following sections provide a CLI and a GUI
approach on how to get this information.

## Ondat GUI - Retrieving a Cluster ID with the Ondat GUI

The Ondat GUI is accessible by default after deployment on port 5705 of any of
Kubernetes worker nodes. For convenience, it's often the easiest to configure
port forward to the service using the following kubectl incantation (this will
block your current terminal session till the port-forward is stopped):

```
$ kubectl port-forward -n storageos svc/storageos 5705
```

The Ondat GUI can then be accessed from `http://localhost:5705` using the default
`storageos-api` secret defined during the installation as credentials (for
example: login: storageos / password: storageos) when using the
[Self-Evaliation Guide](/docs/self-eval).

Depending on the environment, connecting to the localhost might not work when
using a remote administration machine. If this host has a private or public IP,
this IP can be set with the address parameter as such: 

```
$ kubectl port-forward -n storageos svc/storageos 5705 --address 10.20.20.20
```

The Ondat GUI can then be accessed from `http://10.20.20.20:5705`  As an
alternative, you may prefer to use an Ingress controller. You can retrieve the
Ondat cluster by browsing the __Licence__ page as shown below:

![license](/images/docs/concepts/licensing.png)

## Ondat GUI - Obtaining a Licence via the GUI 

Contact Ondat Customer Success team via getstarted@ondat.io and provide the
following information:
- **First** and **last** name
- **Company** **name** and **role** (optional for Personal licence, mandatory
  for Commercial licence)
- **Cluster ID**

In return to the registration, you will receive a licence file with a content
similar to this one:

```
clusterCapacityGiB: 5120 
clusterID: 164237eb-f88a-4bb8-a7cf-a23d468e07c0 
customerName: storageos
expiresAt: "2021-11-15T14:00:00Z" 
features:
- nfs
kind: project

------------- LICENCE SIGNATURE -------------
KyjNleTcdmieZVLmZ/rg0SzdAM7I/CH0j22FIFJJSJaeB71OvQrTMtHGyL5TSFNMrEGbyh1HQlDgZb5A
V1HyjBlS3LjoB/MoagulTxIlZh/R8eRXCOQ46qNZ8Yb7+dHLdCVXBnRqZT11hLqZsMqIeO1y9f5dw65H
kvl6vWW7YIS9r655S25jMMU7brrGDQVdjvU7tSA74BrnzDFHu7/poopIuFqcxZc/NLrKp/akkvyZI5Ex
1wH7D4onjVG2pgi30Kia+mjbI1B9pxQyRppQQ4hNXy4qBUUNMFh0menh0wHdQoM1VLU4Il22PrkeICV0
NaalLsK/96bJov6tpbg96g==
```

## Ondat GUI - Applying a Licence via the Ondat GUI To apply a licence:
1.  Browse the __Licence__ page of the Ondat GUI
1.  Click the __Upgrade__ button, for the specific licence level you purchased
1.  Paste the licence key into the pop-up window
1.  To apply the license click __Upgrade__

> Note: It is crucial to paste all the licence text into the pop-up and not
> just the signature. Keep in mind that the encoding of the file must not
> change.

![Apply Licence Key](/images/docs/operations/licensing/apply-licence-key.png)

## Ondat CLI - Retrieving a cluster ID via the Ondat CLI

For the purpose of this document, it is assumed that the Ondat CLI has been deployed locally on
the same machine hosting kubectl. To retrieve the cluster ID using the Ondat
CLI, perform the following:

```
$ storageos get cluster
ID:               704dd165-9580-4da4-a554-0acb96d328cb
Licence:
  expiration:     2021-03-25T13:48:46Z (1 year from now)
  capacity:       5.0 TiB
  kind:           professional
  customer name:  storageos
Created at:       2020-03-25T13:48:33Z (1 hour ago)
Updated at:       2020-03-25T13:48:46Z (1 hour ago)
```

N.B. All of this string is necessary to activate a licence - not just the
signature.

 ## Ondat CLI - Obtaining a Licence via the CLI

Contact Ondat Customer Success team via getstarted@ondat.io and provide the
following information:
* **First** and **last** name
* **Company** **name** and **role** (optional for Personal licence, mandatory
  for Commercial licence)
* **Cluster ID**

In return to the registration, you will receive a licence file with a content
similar to this one:

```
clusterCapacityGiB: 5120
clusterID: 164237eb-f88a-4bb8-a7cf-a23d468e07c0
customerName: storageos
expiresAt: "2021-11-15T14:00:00Z"
features:
- nfs
kind: project

------------- LICENCE SIGNATURE -------------
KyjNleTcdmieZVLmZ/rg0SzdAM7I/CH0j22FIFJJSJaeB71OvQrTMtHGyL5TSFNMrEGbyh1HQlDgZb5A
V1HyjBlS3LjoB/MoagulTxIlZh/R8eRXCOQ46qNZ8Yb7+dHLdCVXBnRqZT11hLqZsMqIeO1y9f5dw65H
kvl6vWW7YIS9r655S25jMMU7brrGDQVdjvU7tSA74BrnzDFHu7/poopIuFqcxZc/NLrKp/akkvyZI5Ex
1wH7D4onjVG2pgi30Kia+mjbI1B9pxQyRppQQ4hNXy4qBUUNMFh0menh0wHdQoM1VLU4Il22PrkeICV0
NaalLsK/96bJov6tpbg96g==
```

## Ondat CLI  - Applying a licence via the CLI

The following command will apply the licence key stored in
`/path/to/storageos-licence.dat`:

```
$ storageos apply licence --from-file /path/to/storageos-licence.dat
```

For more information refer to the licence
[CLI command](/docs/reference/cli) reference documentation.
