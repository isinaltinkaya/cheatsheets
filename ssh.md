* ### To connect a server without password [(details)](https://www.ssh.com/ssh/copy-id)

`ssh-copy-id user@server`

If it still asks for password, run with `ssh -v`.
e.g. if it says

```
debug1: Unspecified GSS failure.  Minor code may provide more information
No Kerberos credentials available (default cache: FILE:/tmp/asdasd)
```

Run `klist` on the host machine

```
$ klist
Ticket cache: KEYRING:persistent:00:krb_ccache_asdasd
Default principal: asdasd@STH.DOMAIN

Valid starting       Expires              Service principal
DATE  DATE  krbtgt/STH.DOMAIN@STH.DOMAIN
	renew until DATE
```


on client machine run

```
kinit asdasd@STH.DOMAIN
```


