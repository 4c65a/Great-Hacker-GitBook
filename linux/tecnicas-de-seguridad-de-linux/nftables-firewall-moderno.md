# nftables: Firewall Moderno

`nftables` es una herramienta que filtra paquetes y los clasifica, actuando como un firewall para sistemas Linux. Es el sustituto directo de `iptables`, `ip6tables`, `arptables` , unificando todos estos frameworks en una sola solución más limpia, estructurada y eficiente. Su función es controlar el tráfico de red, permitiendo o bloqueando conexiones según reglas que el administrador define. Así, protege el sistema, organiza el flujo de datos y previene accesos no deseados.

***

## Comandos Básicos de nftables

**Mostrar todas las cadenas existentes**

```bash
nft list chains
```

**Ver todas las reglas de la tabla**

```bash
nft list table inet filter
```

**Ver reglas con identificadores**

```bash
nft -a list table inet filter
```

**Exportar configuración en JSON**

```bash
nft export json
```

**Exportar configuración en XML**

```bash
nft export xml
```

**Ver todo el ruleset**

```bash
nft list ruleset
```

**Vaciar todas las reglas del sistema:**

```bash
nft flush ruleset
```

**Vaciar una tabla específica:**

```bash
nft flush table inet filter
```

***

**Crear tabla y cadenas básicas**

```bash
sudo nft add table inet filter
```

```bash
sudo nft add chain inet filter input { type filter hook input priority 0\; }
```

```bash
sudo nft add chain inet filter forward { type filter hook forward priority 0\; }
```

***

**Agregar una regla al final de la cadena `input`**

```bash
sudo nft add rule inet filter input tcp dport 22 accept
```

**Agregar con nombre del servicio**

```bash
sudo nft add rule inet filter input tcp dport ssh accept
```

**Insertar al inicio de la cadena**

```bash
sudo nft insert rule inet filter input tcp dport 22 accept
```

**Insertar antes del handle 3**

```bash
sudo nft insert rule inet filter input position 3 tcp dport 636 accept
```

**Insertar después del handle 3**

```bash
sudo nft add rule inet filter input position 3 tcp dport 80 accept
```

***

**Reglas comunes de filtrado**

**Descarta paquetes con estado de conexión inválido**

```bash
sudo nft add rule inet filter input ct state invalid drop
```

**Permite todo el tráfico entrante desde la interfaz de loopback**

```bash
sudo nft add rule inet filter input iifname lo accept
```

**Permite paquetes que son parte de una conexión ya establecida o relacionadas**

```bash
sudo nft add rule inet filter input ct state established,related accept
```

**Permite tráfico entrante al puerto 80**

```bash
sudo nft add rule inet filter input tcp dport 80 accept
```

**Permite tráfico entrante al puerto 443**

```bash
sudo nft add rule inet filter input tcp dport 443 accept
```

**Bloquea todo el tráfico entrante que no haya sido explícitamente permitido antes**

```bash
sudo nft add rule inet filter input drop
```

***

**Usar sets para múltiples puertos**

```bash
sudo nft add set inet filter allowed_ports { type inet_service\; elements = { 22,80,443 } }
```

```bash
sudo nft add rule inet filter input tcp dport @allowed_ports accept
```

**Detectar paquetes sin flags**

```bash
sudo nft add rule inet filter input tcp flags == 0x0 drop
```

**Prevenir anomalías TCP**

```bash
sudo nft add rule inet filter input tcp flags all == fin,syn,rst,psh,ack,urg drop
```

**Limitar tráfico sospechoso:**

```bash
sudo nft add rule inet filter input tcp flags != syn ct state new counter log prefix "SUSPICIOUS: " level warning
```

**Limitar conexiones por segundo**

```bash
sudo nft add rule inet filter input limit rate 15/second counter drop
```

**Bloquear IPs en set**

```bash
sudo nft add set inet filter banned_ips { type ipv4_addr\; elements = { 103.0.0.0/8,185.220.101.0/24 } }
```

```bash
sudo nft add rule inet filter input ip saddr @banned_ips drop
```

***

**NAT y redirección**

```bash
sudo nft add table ip nat
```

```bash
sudo nft add chain ip nat postrouting { type nat hook postrouting priority 100\; }
```

```bash
sudo nft add rule ip nat postrouting oifname "eth0" ip saddr 192.168.10.0/24 masquerade
```

***

**Guardar reglas y hacerlas persistentes:**

```bash
sudo nft list ruleset > /etc/nftables.conf
```

```bash
sudo systemctl enable nftables
```

***

#### Para mas información

{% embed url="https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/7/html/security_guide/sec-creating_and_managing_nftables_tables_chains_and_rules#sec-Inserting-a-rule-at-a-specific-position-of-an-nftables-chain" %}
