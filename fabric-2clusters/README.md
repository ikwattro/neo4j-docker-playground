# Fabric with 2 clusters

- 1 Fabric instance
- 2 3xcores Neo4j clusters

## Launch

Launch cluster 1

```
docker-compose --profile clustera up -d
```

Wait cluster is ready

Launch cluster 2

```
docker-compose --profile clusterb up -d
```

Wait cluster is ready

Launch Fabric

```
docker-compose --profile fabric up -d
```


## Commands

Go to cluster 1, check who is leader for system db

Go to leader, create `red` db, write one Person on red db leader

Do same for cluster 2, but create a `blue` db instead

Go to Fabric instance on http://localhost:7474

use the fabric graph

```
:use matrix
```

Query that collects data from the two clusters

```
USE matrix.blue
MATCH (n) RETURN n
UNION
USE matrix.red
MATCH (n) RETURN n
```