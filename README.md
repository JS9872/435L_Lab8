# EECE 435L Lab 8 — Docker containers and images

Student: Joey Sade (202305993)

The first image runs the Lab 5 Flask user API on port 5000. The second runs the same API on port 3000 and adds `GET /api/get_users`, returning a JSON list of names from the SQLite users table. The database is created on first run and is stored inside each container unless a volume is mounted.

Docker image tags cannot contain two colons, so the handout's `0.0.1:RELEASE` and `0.0.2:RELEASE` are represented as `0.0.1-RELEASE` and `0.0.2-RELEASE`. The repository owner `js9872` is used as the image namespace; replace it if the AUB username differs.

```powershell
docker build -f Dockerfile.v1 -t js9872/lab8-joey_sade:0.0.1-RELEASE .
docker build -f Dockerfile.v2 -t js9872/lab8-joey_sade:0.0.2-RELEASE .
docker run --name lab8-v1 -p 5000:5000 -d js9872/lab8-joey_sade:0.0.1-RELEASE
docker run --name lab8-v2 -p 3000:3000 -d js9872/lab8-joey_sade:0.0.2-RELEASE
```

Check `http://localhost:5000/api/users` and `http://localhost:3000/api/get_users`. To populate data, POST JSON with `name`, `email`, `phone`, `address`, and `country` to `/api/users/add` on either port. The containers have independent databases.

Activity 1 commands:

```powershell
docker ps -a
docker stop lab8-v1
docker logs lab8-v1
```

`docker ps -a` lists all containers, including stopped ones. `docker stop` sends a termination signal to the named container. `docker logs` prints that container's standard output and error. These commands use a **container name or ID**, even though the handout says image name.
