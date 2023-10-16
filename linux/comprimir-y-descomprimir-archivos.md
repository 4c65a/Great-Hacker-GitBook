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

# Comprimir y descomprimir archivos

### Tar

#### Para comprimir&#x20;

```bash
tar -cvf TEST.tar test test1 test2
```

#### Listar el contenido

```bash
tar -tvf TEST.tar
```

#### Descomprimir

```bash
tar -xvf TEST.tar
```

#### Para comprimir archivo con .tar.gz o .tgz utilizar gzip o gunzip

```bash
gzip -c TEST.tar > TEST.tar.gzc
```

#### Para descomprimir

```bash
gunzip TEST.tar.gz
```

#### Para comprimir un archivo con la extensión .tar.bz2

```
bzip2 -c archivo.tar > archivo.tar.bz2
```

```
bzip2 -d archivo.tar.bz2
```

which uses the extension .tar.z

Linux >compress HackersArise.\* Linux >uncompress HackersArise.\*

```
// Some code
```

```
// Some codec
```
