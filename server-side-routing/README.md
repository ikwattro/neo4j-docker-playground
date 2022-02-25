# Server Side Routing

- 3 X Neo4j Core with no ports exposed
- 1 X Neo4j Core with ports exposed
- 1 Read Replica
- Server Side Routing enabled

```bash
docker-compose up -d
```

Tail the logs until all cores and the read replica are up :

```bash
docker-compose logs --tail 100 -f
```

The 3 cores are not available outside of the docker network and no ports are mapped, only the read replica is exposed.

Once up, go to `localhost:57474` and log in with `neo4j/password` using the `neo4j://` scheme.

Create a node 

```
CREATE (n:Test)
```

Without server side routing, creating the node would fail since the client would try to load balance to the leader but the leader is not available.

Tear down 

```bash
docker-compose -f compose-ssr.yml down --volumes --remove-orphans
```