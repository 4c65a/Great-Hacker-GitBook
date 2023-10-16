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

bzip2, which uses the extension .tar.bz2.

Linux >bzip2 HackersArise.\* Linux >bunzip2 HackersArise.\*

```
// Some code
```

```
// Some code
```

which uses the extension .tar.z

Linux >compress HackersArise.\* Linux >uncompress HackersArise.\*

```
// Some code
```

```
// Some codec
```
