# Fabric Single instance example

Launch db 

```
docker-compose up -d
```

2 databases are configured and seeded, `movies` and `users`

Connect to Neo4j on http://localhost:17474 and use the `matrix` fabric 

```
:use matrix
```

And fetch nodes from both dbs

```
USE movies
MATCH (n:Person)
RETURN n LIMIT 5
UNION
USE users
MATCH (n)
RETURN n
```

```
╒═════════════════════════════════════════╕
│"n"                                      │
╞═════════════════════════════════════════╡
│{"born":1964,"name":"Keanu Reeves"}      │
├─────────────────────────────────────────┤
│{"born":1967,"name":"Carrie-Anne Moss"}  │
├─────────────────────────────────────────┤
│{"born":1961,"name":"Laurence Fishburne"}│
├─────────────────────────────────────────┤
│{"born":1960,"name":"Hugo Weaving"}      │
├─────────────────────────────────────────┤
│{"born":1967,"name":"Lilly Wachowski"}   │
├─────────────────────────────────────────┤
│{"name":"Luanne"}                        │
├─────────────────────────────────────────┤
│{"name":"Christophe"}                    │
├─────────────────────────────────────────┤
│{"name":"Sergio"}                        │
├─────────────────────────────────────────┤
│{"name":"Andrea"}                        │
└─────────────────────────────────────────┘
```