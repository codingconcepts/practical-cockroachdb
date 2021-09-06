# Multi-node cluster

## Node 1

```
$ cockroach start \
  --insecure \
  --store=node2 \
  --listen-addr=localhost:26257 \
  --http-addr=localhost:8080 \
  --join=localhost:26257,localhost:26258,localhost:26259
```

## Node 2

```
$ cockroach start \
  --insecure \
  --store=node2 \
  --listen-addr=localhost:26258 \
  --http-addr=localhost:8081 \
  --join=localhost:26257,localhost:26258,localhost:26259
```

## Node 3

```
$ cockroach start \
  --insecure \
  --store=node3 \
  --listen-addr=localhost:26259 \
  --http-addr=localhost:8082 \
  --join=localhost:26257,localhost:26258,localhost:26259
```

## Init

```
$ cockroach init --insecure --host=localhost:26257
Cluster successfully initialized
```

## Connect

```
$ cockroach sql --insecure --host=localhost:26257
```


```
cockroach start \
  --insecure \
  --store=node1 \
  --listen-addr=localhost:26257 \
  --http-addr=localhost:8080 \
  --locality=region=us-east-1,zone=us-east-1a \
  --join 'localhost:26257, localhost:26258, localhost:26259, localhost:26260, localhost:26261, localhost:26262, localhost:26263, localhost:26264, localhost:26265'
```