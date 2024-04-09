TEST : https://your_domain/v2

http://<IP>:5000/v2/
{}

## ดู image ทั้งหมดที่มีอยู่ใน catalog

http://<IP>:5000/v2/\_catalog

```
{
  "repositories": ["kong", "postgres"]
}

```

## ดู tag ทั้งหมดของ image ที่สนใจ

http://<IP>:5000/v2/kong/tags/list

```
{
  "name": "kong",
  "tags": ["latest"]
}

```

## delete image

เราต้องใช้เลข digest ในการลบ image ที่เราไม่ใช้ ง่ายที่สุดคือ pull image มาใหม่เพื่อดูเลข digest

❯ docker pull <IP>:5000/kong
Using default tag: latest
latest: Pulling from kong
Digest: sha256:d40ee6cda8cc90736f6ec07c4f4564a4f05358c70addd45829ab2f7f0f67ed78
Status: Image is up to date for <IP>:5000/kong:latest
<IP>:5000/kong:latest

EX.
docker exec -it <registry container Id> bin/registry garbage-collect /etc/docker/registry/config.yml

docker exec -it f64ca6339f92 bin/registry garbage-collect /etc/docker/registry/config.yml

# server

sudo nano /etc/docker/daemon.json

```
{
    "insecure-registries" : ["http://<IP>:5000"]
}
```

sudo service docker restart

---

# mac

แก้ Docker Engine
Docker Desktop -> Settings -> Docker Engine
"insecure-registries" : ["http://<IP>:5000"],

```
{
  "builder": {
    "gc": {
      "defaultKeepStorage": "20GB",
      "enabled": true
    }
  },
  "experimental": false,
  "insecure-registries": [ "http://<IP>:5000" ]
}
```

---

docker tag test-image your_domain/test-image
docker push your_domain/test-image

---

docker tag postgres <IP>:5000/postgres  
docker push <IP>:5000/postgres

---

docker tag kong <IP>:5000/kong  
docker push <IP>:5000/kong
