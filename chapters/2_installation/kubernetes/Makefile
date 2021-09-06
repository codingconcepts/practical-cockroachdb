apply:
	kubectl apply -f 1_pod-disruption-budget.yaml
	kubectl apply -f 2_stateful-set.yaml
	kubectl apply -f 3_private-service.yaml
	kubectl apply -f 4_public-service.yaml

init:
	kubectl create -f init.yaml

delete:
	kubectl delete -f 4_public-service.yaml
	kubectl delete -f 3_private-service.yaml
	kubectl delete -f 2_stateful-set.yaml
	kubectl delete -f 1_pod-disruption-budget.yaml
	kubectl delete -f init.yaml

connect:
	kubectl run cockroachdb --rm -it \
		--image=cockroachdb/cockroach:v21.1.7 \
		--restart=Never \
		-- sql \
		--insecure \
		--host=cockroachdb-public

forward_http:
	kubectl port-forward service/cockroachdb-public 8080

forward_tcp:
	kubectl port-forward service/cockroachdb-public 26257