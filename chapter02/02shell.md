# Docker como shell

Podemos ingresar al contenedor docker para ejecutar los comandos que estén disponibles en la imágen que utilizamos para correrlo.

```
$ docker run -it debian bash
```

donde:

''-i'' crea una sesión interactiva

''-t'' ofrece una terminal (tty)

y la //imagen// que utilizará es un `debian` mínimo y ejecutará el comando `bash`, dando como resultado un shell:

```
root@ce1a1c7bf990:/#
root@ce1a1c7bf990:/# pwd
/
root@ce1a1c7bf990:/# ps ax
  PID TTY      STAT   TIME COMMAND
    1 ?        Ss     0:00 bash
    6 ?        R+     0:00 ps ax
root@ce1a1c7bf990:/# exit
exit
```

---

{{Seguir}} [[Docker autoejecutable]]


