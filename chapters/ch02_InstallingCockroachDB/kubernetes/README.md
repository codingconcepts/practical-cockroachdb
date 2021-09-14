# ch02_InstallingCockroachDB

## Kubernetes

To install CockroachDB into a Kubernetes cluster, run the following commands:
```
$ kubectl apply -f 1_pod-disruption-budget.yaml
$ kubectl apply -f 2_stateful-set.yaml
$ kubectl apply -f 3_private-service.yaml
$ kubectl apply -f 4_public-service.yaml

$ kubectl create -f init.yaml
```

To conect to a CockroachDB cluster that's running in Kubernetes, run the following command:
```
$ kubectl run cockroachdb --rm -it \
	--image=cockroachdb/cockroach:v21.1.7 \
	--restart=Never \
	-- sql \
        --insecure \
        --host=cockroachdb-public
```

To view the CockroachDB management console (UI) for the cluster running in Kubernetes, run the following command, then visit http://localhost:8080:
```
$ kubectl port-forward service/cockroachdb-public 8080
```

To connect to the CockroachDB database from the command line or from your application, run the following command:
```
$ kubectl port-forward service/cockroachdb-public 26257
```

To uninstall CockroachDB from a Kubernetes cluster, run the following commands:
```
$ kubectl delete -f 4_public-service.yaml
$ kubectl delete -f 3_private-service.yaml
$ kubectl delete -f 2_stateful-set.yaml
$ kubectl delete -f 1_pod-disruption-budget.yaml

$ kubectl delete -f init.yaml
```