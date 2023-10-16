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

```bash
bzip2 -c TEST.tar > TEST.tar.bz2
```

#### Para descomprimir

```bash
bzip2 -d TEST.tar.bz2
```

#### Para comprimir un archivo con la extensión .tar.z

```bash
compress TEST.tar
```

#### Para descomprimir

```bash
uncompress TEST.tar.z
```

