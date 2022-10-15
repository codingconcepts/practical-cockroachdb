# Multi-node cluster

State the first node in the cluster by running the following command:
```
$ cockroach start \
  --insecure \
  --store=node1 \
  --listen-addr=localhost:26257 \
  --http-addr=localhost:8080 \
  --join=localhost:26257,localhost:26258,localhost:26259
```

State the second node in the cluster by running the following command:
```
$ cockroach start \
  --insecure \
  --store=node2 \
  --listen-addr=localhost:26258 \
  --http-addr=localhost:8081 \
  --join=localhost:26257,localhost:26258,localhost:26259
```

State the third node in the cluster by running the following command:
```
$ cockroach start \
  --insecure \
  --store=node3 \
  --listen-addr=localhost:26259 \
  --http-addr=localhost:8082 \
  --join=localhost:26257,localhost:26258,localhost:26259
```

Initialise the cluster by running the following command:
```
$ cockroach init --insecure --host=localhost:26257
```

Connect to the cluster on the command line by running the following command:
```
$ cockroach sql --insecure --host=localhost:26257
```