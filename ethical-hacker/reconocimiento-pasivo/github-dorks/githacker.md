---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Githacker

#### Git <a href="#user-content-git" id="user-content-git"></a>

```
githacker.py -u https://github.com/nombre-usuario/repositorio.git
```

Buscar contraseñas filtradas en repositorios de GitHub:

```
githacker.py -u <usuario> -t <token> -s <org/user> -k password,token,ssh
```

Buscar archivos con información sensible, como credenciales y claves de API

```
githacker.py -u <usuario> -t <token> -s <org/user> -k aws_access_key_id,aws_secret_access_key,api_key,client_secret,client_id,authorization,passwd,pass
```

Buscar archivos con extensiones específicas en todos los repositorios de una organización:

```
githacker.py -u <usuario> -t <token> -s <org/user> -x yml,config,json,pem,sql,txt
```

Buscar repositorios privados que puedan contener información sensible

```
githacker.py -u <usuario> -t <token> --all --type private -k secret,token,passwd,key,id
```

Buscar archivos con datos sensibles que hayan sido eliminados pero aún se puedan encontrar en el historial de commits

```
githacker.py -u <usuario> -t <token> -s <org/user> -k password,apikey,secret,token,username,email,aws_access_key_id,aws_secret_access_key --all --include-history
```

\
