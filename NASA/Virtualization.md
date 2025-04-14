# Virtualization (Week 9)

**Full virtualization**: no access to hardware from guest OS, no guest OS modification is needed
**Paravirtualization**: contrary

![[Pasted image 20250414095554.png]]

## docker

add user to `docker` group:
```
sudo groupadd docker
sudo usermod -aG docker $USER
newgrp docker
```
