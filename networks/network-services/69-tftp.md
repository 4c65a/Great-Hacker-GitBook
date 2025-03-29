# 69:TFTP

## ¿Que es TFTP

TFTP es un protocolo simple de transferencia de archivos que permite a un cliente obtener o colocar un archivo en un host remoto. Utiliza UDP. Un puerto predeterminado es el 69.

**Su puerto por defecto:**

```
PORT   STATE SERVICE REASON
69/udp open  tftp    script-set
```

## Escanear

```
nmap -sU --script tftp-enum -p 69 <target-ip>
```

```
nmap -n -Pn -sU -p69 -sV --script tftp-enum <IP>
```

### Script

```
nmap -sU --script tftp-enum -p 69 <target-ip>
```

<mark style="color:red;">**Recursos**</mark>

{% embed url="https://book.hacktricks.xyz/network-services-pentesting/69-udp-tftp" %}
