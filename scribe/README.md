# Scribe Demos

Scribe is a tool to replicate Kubernetes Persistent Volumes across Namespaces, StorageClasses, or Clusters.
This folder holds scripts to show off scribe.
Scribe Operator should be installed in a Kubernetes or OpenShift cluster to run these demos.
If using Snapshot Copy Method, cluster should have CSI driver and StorageClass with Snapshotting capabilities.

[Scribe Documentation](https://scribe-replication.readthedocs.io/en/latest/index.html)

[Scribe Repository](https://github.com/backube/scribe)

# Notes on Cross Cluster Usage:

Scribe command uses Kubernetes contexts to distinguish between clusters.
If not familiar with using Kubernetes contexts, it is recommended to:

*  Copy Kubeconfigs to a new file, to ensure you always have your original Kubeconfig to go back to.
*  Here are useful `kubectl config` commands:

```console
$ kubectl config get-contexts
$ kubectl config use-context <context>
$ kubectl --context <some-context> <kubectl-command>
```

You'll want to create users in your cluster before using Scribe,
rather than use the temporary `kubeadmin` user or the `system:admin` user.

For testing purposes, I recommend using this [test ldap server](https://www.forumsys.com/tutorials/integration-how-to/ldap/online-ldap-test-server/)

If running in OpenShift 4.x, this will give you a user with cluster-admin privileges:
* See [ldap.yaml](ldap.yaml)
* `$ oc apply -f ldap.yaml`
* (logged in as system-admin): `$ oc adm policy add-cluster-role-to-user cluster-admin newton`
* `$ oc login -u newton -p password`

After you have users, you may then:

`$ export KUBECONFIG=~/kubeconfig1:~/kubeconfig2`

