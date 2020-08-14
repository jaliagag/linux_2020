# Para Dori

## SSH + GitHub

Lo primero que hice fue correr 'ssh-keygen' y eso generó en ~/.ssh dos archivos:

- id_rsa - con la clave privada
- id_rsa.pub - con la clave pública

Entré en mi cuenta de github y la subí y "sincornicé" con mi cuenta de github - la aceptó pero sigo sin poder hacer el push.

Corrí este comando para correr al ssh-agent en el background

```sh
$ eval "$(ssh-agent -s)"
```

Corrí este comando para agregar mi identidad:

```sh
$ ssh-add ~/.ssh/id_rsa

```

Capítulo 2:

Generé un token de desarrollador nuevo en github. Lo guardé en la máquina ubuntu y lo pasé como contraseña a la hora de hacer el push.
