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

# Explotaciones SMTP

Se puede aprovechar los  servidores SMTP inseguros para enviar spam y realizar phishing y otros ataques basados ​​en correo electrónico. SMTP es un protocolo de servidor a servidor.

puertos TCP estándar asociados con los diferentes protocolos de correo. Algunos de los puertos clave incluyen:

* **SMTP (Simple Mail Transfer Protocol):**
  * Puerto TCP 25: Predeterminado para comunicaciones no cifradas.
  * Puerto TCP 465: Registrado por la IANA para SMTP sobre SSL (SMTPS), aunque ha quedado obsoleto en favor de STARTTLS.
  * Puerto TCP 587: Utilizado para SMTP seguro (SSMTP) mediante STARTTLS.
* **POP3 (Post Office Protocol 3):**
  * Puerto TCP 110: Predeterminado para comunicaciones no cifradas.
  * Puerto TCP 995: Predeterminado para comunicaciones cifradas.
* **IMAP (Internet Message Access Protocol):**
  * Puerto TCP 143: Predeterminado para comunicaciones no cifradas.
  * Puerto TCP 993: Predeterminado para comunicaciones cifradas mediante SSL/TLS.

## _SMTP open Relay_&#x20;

_SMTP open Relay_ es el término utilizado para un servidor de correo electrónico que acepta y _retransmite_ (es decir, envía) correos electrónicos de cualquier usuario. Es posible abusar de estas configuraciones para enviar correos electrónicos falsificados, spam, phishing y otras estafas relacionadas con el correo electrónico.&#x20;

```
nmap --script smtp-open-relay.nse 10.1.2.14
```

### Se conecta al servidor  mediante **telnet** :puerto 25

```bash
telnet 192.168.78.8 25
```

1.  ```plaintext
    VRFY sys
    ```

    **Respuesta del Servidor:**

    ```plaintext
    252 2.0.0 sys
    ```

    La respuesta "252 2.0.0 sys" indica que el servidor reconoce el usuario "sys".
2.  **Comando:**

    ```plaintext
    VRFY admin
    ```

    **Respuesta del Servidor:**

    ```plaintext
    550 5.1.1 <admin>: Recipient address rejected: User unknown in local
    recipient table
    ```

    La respuesta "550 5.1.1 \<admin>: Recipient address rejected: User unknown in local recipient table" indica que el usuario "admin" no es conocido en la tabla local de destinatarios.
3.  **Comando:**

    ```plaintext
    VRFY root
    ```

    **Respuesta del Servidor:**

    ```plaintext
    252 2.0.0 root
    ```

    La respuesta "252 2.0.0 root" indica que el servidor reconoce el usuario "root".
4.  **Comando:**

    ```plaintext
    VRFY omar
    ```

    **Respuesta del Servidor:**

    ```plaintext
    252 2.0.0 omar
    ```

La herramienta `smtp-user-enum`facilita la automatización del proceso de recopilación de información en servidores SMTP.

#### Ejemplos

```
smtp-user-enum -M VRFY -U users.txt -t 10.0.0.1
smtp-user-enum -M EXPN -u admin -t 10.0.0.1
smtp-user-enum -M RCPT -U users.txt -T mail-server-ips.txt
smtp-user-enum -M EXPN -D google.com -U users.txt -t 10.0.0.1
smtp-user-enum -M VRFY -u omar -t 192.168.78.8
```
