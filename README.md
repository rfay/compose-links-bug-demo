Bug demo for docker-compose 2.1.1 `links` problem

1. `docker network create test`
2. In each directory (`one` and `two`) `docker-compose up` - You'll now have two identical services on the same network.
3. Use `docker exec one-web-1 ping -c1 db` to see the name resolution going on inside `one-web-1`. 

On compose v1 and up through v2.0.1 you'll see consistent name lookup, always coming out to be the `db` service one-db-1. On compose v2.1.1, you'll see it flip back and forth between `one-db-1` and `two-db-1` - it's inconsistent round-robin behavior, so you may have to hit `docker exec one-web-1 ping -c1 db` a few times to see it.
