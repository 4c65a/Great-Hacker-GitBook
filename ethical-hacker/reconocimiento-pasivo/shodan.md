# Shodan

Shodan es un motor de búsqueda que permite encontrar dispositivos conectados a Internet. Este motor de búsqueda recopila información sobre los dispositivos conectados a Internet, como su dirección IP, su ubicación, el sistema operativo que utilizan, los puertos que tienen abiertos.

{% embed url="https://cli.shodan.io/" %}

## Download

```
```

## Host enumeracion

```
shodan host 1.1.1.1
```

```
shodan host 13.123.15.21
```

## Parse DataSet

{% embed url="https://help.shodan.io/mastery/working-with-shodan-data-files" %}

```
shodan myip
```

```
shodan parse .json
```

## Search Query

{% embed url="https://www.shodan.io/search/examples" %}

```
shodan search ssh
```

## Scan&#x20;

```
shodan scan internet
```

```
shodan scan list
```

```
shodan scan protocols
```

```
shodan scan status
```

```
shodan scan submit 
```

## Stats

```
shodan stats ftp
```

