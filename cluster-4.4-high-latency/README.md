# 4.4 cluster with high latency traffic

Uses a custom build of the 4.4 Docker image with tooling for simulating latency in network traffic.

Run `docker compose up -d`

**Check which server is the leader for the neo4j database**

- Go to the browser localhost:17474
- Login with neo4j/password
- Run `show databases`
- Check who is the leader

**Connect to the leader**

- Open the browser of the instance being leader and connect with **BOLT** (NB: browsers run on ports 17474,27474,37474)

**Add latency to other members**

- Check the docker container names and replace accordingly in next commands : `docker ps -a | grep cluster-44-high`

- Run the following command using the follower container names : `docker exec cluster-44-high-latency-core3-1 tc qdisc add dev eth0 root netem delay 5000ms` (this adds 5 seconds latency on the followers)


- To reset to the normal latency, run the following command to the instances you modified : `docker exec cluster-44-high-latency-core1-1 tc qdisc del dev eth0 root netem`

