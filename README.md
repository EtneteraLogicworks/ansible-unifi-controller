# Role unifi-controller

Role nasadí [UniFi controller](https://www.ui.com/download/unifi/) pro Debian.
Dále je nastavena reverzní proxy (Apache), aby bylo možné snadno nasadit validní
TLS certifikát pro HTTPS a používat běžný port 443 místo 8433 na kterém poslouchá
samotný controller.

Předpokládáme nasazení do prostředí Debian 9 z důvodu závislostí. Balíček `unifi`
totiž vyžaduje pro svůj běh prostředí Java 8 a MongoDB 3.4. Obě technologie jsou
zastaralé a zprovoznit je v Debian 10 a novějších vyžaduje vyřešit mnoho překážek.

UniFi controller využívá více síťových portů viz [dokumentace](https://help.ui.com/hc/en-us/articles/218506997-UniFi-Ports-Used).

## Proměnné

Role `unifi-controller` se konfiguruje pomocí slovníku `unifi`:

| Proměnná                     | Povinná | Výchozí           | Popis |
| ---------------------------- | ------- | ----------------- | ----- |
| vhost                        | ne      |                   | Slovník s parametry pro apache virtual host |
| .name                        | ne      | unifi             | Identifikátor vhosta (použitý pro jména souborů) |
| .site_name                   | ne      | unifi.example.com | ServerName virtual hosta |
| .aliases                     | ne      |                   | Pole aliasů virtual hosta |
| .admin_mail                  | ne      | {{ admin_mail }}  | Email na admina webu |
| .https_enabled               | ne      | true              | Zapne HTTPS |
| .https_letsencrypt           | ne      | false             | Zapne získávání LE certifikátů |
| .https_redirect              | ne      | false             | Zapne Redirect HTTP -> HTTPS |
| .cert                        | ne      | snakeoil.pem      | Cesta k certifikátu virtual hosta |
| .key                         | ne      | snakeoil.key      | Cesta ke klíči virtual hosta |
| .chain                       | ne      |                   | Cesta k souboru s certifikáty mezilehlých autorit |
