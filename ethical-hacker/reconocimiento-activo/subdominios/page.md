# Page

### [step by step](https://github.com/Lean-b/BugBounty/blob/main/Recon.md#step-by-step) <a href="#user-content-step-by-step" id="user-content-step-by-step"></a>

Link = [https://security.snyk.io/](https://security.snyk.io/) [https://www.cve.org/](https://www.cve.org/)

#### [Phase One](https://github.com/Lean-b/BugBounty/blob/main/Recon.md#phase-one) <a href="#user-content-phase-one" id="user-content-phase-one"></a>

```
subfinder -d example.com >> subdominios.txt
```

```
sublist3r -d example.com  >> subdominios.txt
```

```
amass enum -d example.com -max-dns-queries 120 >> subdominios.txt
```

```
amass enum -passive -d example.com >> subdominios.txt
```

#### [Phase two](https://github.com/Lean-b/BugBounty/blob/main/Recon.md#phase-two) <a href="#user-content-phase-two" id="user-content-phase-two"></a>

```
cat subdominios.txt | httprobe -c 100 >> subdominios2.txt
```

```
cat subdominios2.txt | uniq >> subdominios3.txt
```

```
httpx -l subdominios3.txt -sc | grep 200 >> subdominios4.txt
```

```
httpx -l subdominios4.txt -sc -td
```

[**Option two**](https://github.com/Lean-b/BugBounty/blob/main/Recon.md#option-two)

```
cat subdominios.txt | httprobe -c 100 >> subdominios2.txt
```

```
cat subdominios2.txt | uniq >> subdominios3.txt
```

```
cat subdominios3.txt | httprobe -c 100  > hosts_validos.txt
```

```
httpx -l hosts_validos.txt -sc | grep 200 >> hosts_validos1.txt
```

```
httpx -l hosts_validos1.txt -sc -td >> hosts_validos2.txt
```

```
httpx -l hosts_validos.txt -all-ports 80,443 -title -status-code -web-server > hosts_abiertos.txt
```

_**200**_: Indicate that an HTTP request has been successful and the server will return an answer.

_**301**_: Indicate that an URL request has been moved permanently an a new ubication.

_**404**_: Indicate that a URL request has not been found on the server.

_**500**_: Indicate that an internal server error has occurred and the request could not be completed.

#### [Phase three](https://github.com/Lean-b/BugBounty/blob/main/Recon.md#phase-three) <a href="#user-content-phase-three" id="user-content-phase-three"></a>

```
ffuf -w /usr/share/sectlist -u http://example.com/login.php/FUZZ -p1
```

```
ffuf -w /usr/share/sectlist -u http://example.com/FUZZ  -fc 403,301,302 -c -T 200 -e html,php,txt,zip,jsp -p 2 -r 10 -rate 50
```

```
ffuf -w /usr/share/sectlist -u http://example.com/FUZZ  -T 200 -e html,php,txt,zip,jsp -p 2 -r 10 -rate 50 -maxtime-job 60 -recursion -recursion-depth 2
```

```
nmap -sS -T1 10.10.23.51 --top-ports -V
```

```
nmap -A -F -T1 10.10.23.51 -V
```

#### [Phase four research](https://github.com/Lean-b/BugBounty/blob/main/Recon.md#phase-four-research) <a href="#user-content-phase-four-research" id="user-content-phase-four-research"></a>

[shodan](https://www.shodan.io/search/examples) hostname:example.com

[Censys](https://search.censys.io/)

[wayback](https://archive.org/web/)

[crt.sh](https://crt.sh/)

[Iccan](https://lookup.icann.org/en)

[Hunter](https://hunter.io/?via=untyped\&gclid=Cj0KCQiA0oagBhDHARIsAI-Bbgdh19MSChfD3HpNmtNme0IeOT8W5LZ6Bl\_chGloD9iRTUwhHxwkznkaAmbeEALw\_wcB)

[ONYPHE](https://www.onyphe.io/)

[Netify](https://www.netify.ai/resources/applications)

[grep.app](https://grep.app/)

[Intelligence x](https://intelx.io/)

[Netlas.io](https://app.netlas.io/host/)

```
./waybackurls yahoo.com
```

\*\*\*Searchsploit:\*\*\*Search vulnerability

\*\*\*Wappalyzer:\*\*\*Tools

\*\*\*DoGit:\*\*\*Repositories
