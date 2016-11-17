# User Management

---

## Default runs as root

```
$ docker run -v /bin:/host/bin -it --rm alpine sh
$ whoami
root
$ id
uid=0(root) gid=0(root)
```
- Please **DO NOT** do this

---

## Container root user

- root in container == root outside container
- We do not want this to be the case!
- How can we change this?

![](images/rootUser.png)


---

## Step in the right direction: run as a user

- Use the ``--user`` flag with UID:GID argument

```
$ docker run -v /bin:/host/bin --user 1000:10000 -it --rm alpine sh
$ whoami
whoami: unknown uid 10000
$ id
uid=10000 gid=10000

```

---

## But I still want *root* inside container
![](images/dockerUser.png)

Run a command that needs to look like `root` in the container, without giving
`root` access to the underlying host

---

## Enable user namespaces

- Use the ``--userns-remap`` flag with UID:GID argument


![](images/userNamespaces.png)

---

## Enable user namespaces - common pitfalls
```
$ docker daemon --userns-remap [uid[:gid]]
```
- Will need to re-pull images and re-create volumes due to container resource and image layer permissions
- Leave this feature on in production; switching back and forth should only be done in development

![](images/userNamespace2.png)

---

## Hands-On Exercise && break
www.katacoda.com/docker-training/courses/security-course
- **userns** scenario


---
