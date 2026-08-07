# Cenário 01 — Rede Virtualizada com RIPv2, DNS e HTTP

Projeto de implementação de uma infraestrutura de rede com cinco roteadores, cinco redes locais, servidores DNS, servidores web e máquinas clientes.

A topologia foi desenvolvida inicialmente no Cisco Packet Tracer e posteriormente implementada no Oracle VirtualBox utilizando máquinas Ubuntu Server.

## Objetivos

- Configurar roteamento dinâmico com RIPv2.
- Permitir a comunicação entre diferentes redes locais.
- Implementar resolução de nomes com BIND9.
- Disponibilizar páginas HTTP com Apache2.
- Validar a infraestrutura por meio de testes de conectividade, DNS e HTTP.
- Documentar as configurações e evidências da implementação.

## Tecnologias utilizadas

- Oracle VirtualBox
- Ubuntu Server
- Cisco Packet Tracer
- FRRouting
- RIPv2
- BIND9
- Apache2
- Netplan
- Linux

## Estrutura do repositório

```text
virtualized-network-scenario-1/
├── configs/
│   ├── clients/
│   ├── dns/
│   ├── routers/
│   └── web/
├── docs/
│   └── index.html
├── packet-tracer/
├── virtualbox/
│   ├── clients/
│   ├── routers/
│   ├── servers/
│   └── README.md
└── README.md
```

## Topologia da rede

A infraestrutura utiliza cinco roteadores interligados por enlaces ponto a ponto com máscara `/30`.

Cada roteador também fornece acesso a uma rede local:

| Roteador | Rede local | Gateway |
|---|---|---|
| R1 | `192.168.1.0/24` | `192.168.1.1` |
| R2 | `192.168.2.0/24` | `192.168.2.1` |
| R3 | `192.168.3.0/24` | `192.168.3.1` |
| R4 | `192.168.4.0/24` | `192.168.4.1` |
| R5 | `192.168.5.0/24` | `192.168.5.1` |

### Enlaces entre roteadores

| Enlace | Rede |
|---|---|
| R1 ↔ R2 | `10.1.12.0/30` |
| R1 ↔ R4 | `10.1.14.0/30` |
| R2 ↔ R3 | `10.1.23.0/30` |
| R3 ↔ R5 | `10.1.35.0/30` |
| R4 ↔ R5 | `10.1.45.0/30` |

O protocolo RIPv2 foi utilizado para distribuir as rotas entre os roteadores.

## Servidores web

Foram configurados três servidores Apache2:

| Servidor | Endereço IP | Rede |
|---|---|---|
| WEB1 | `192.168.1.10` | LAN1 |
| WEB2 | `192.168.2.10` | LAN2 |
| WEB3 | `192.168.3.10` | LAN3 |

Cada servidor possui uma página HTML utilizada para identificar o serviço durante os testes com `curl`.

## Servidores DNS

Foram utilizados dois servidores BIND9:

| Servidor | Endereço IP | Rede |
|---|---|---|
| DNS1 | `192.168.1.5` | LAN1 |
| DNS2 | `192.168.4.5` | LAN4 |

A zona utilizada no projeto é:

```text
rede.local
```

### Registros configurados no DNS1

```text
servidor1.rede.local → 192.168.1.10
servidor2.rede.local → 192.168.2.10
```

### Registro configurado no DNS2

```text
servidor3.rede.local → 192.168.3.10
```

## Máquinas clientes

| Cliente | Endereço IP | Gateway | DNS |
|---|---|---|---|
| PC-A | `192.168.4.10/24` | `192.168.4.1` | `192.168.1.5` |
| PC-B | `192.168.5.10/24` | `192.168.5.1` | `192.168.1.5` |
| PC-C | `192.168.5.11/24` | `192.168.5.1` | `192.168.4.5` |

Os clientes foram utilizados para testar conectividade, resolução DNS e acesso aos servidores HTTP.

## Configurações

Os arquivos reais utilizados nas máquinas estão disponíveis nas seguintes pastas:

- [Configurações dos clientes](configs/clients/)
- [Configurações dos roteadores](configs/routers/)
- [Configurações dos servidores DNS](configs/dns/)
- [Configurações dos servidores web](configs/web/)

A pasta `configs/routers/` contém os arquivos Netplan e FRRouting dos roteadores R1 até R5.

A pasta `configs/dns/` contém as configurações do Netplan, do BIND9 e dos arquivos de zona.

A pasta `configs/web/` contém as configurações de rede e as páginas HTML dos servidores Apache2.

## Evidências da implementação

Os testes realizados no VirtualBox estão documentados no arquivo abaixo:

[Ver implementação e evidências no VirtualBox](virtualbox/README.md)

As evidências incluem:

- tabelas de roteamento;
- rotas aprendidas pelo RIPv2;
- comunicação entre redes diferentes;
- testes de ping;
- consultas DNS com `nslookup`;
- acesso HTTP com `curl`;
- status dos serviços Apache2.

## Simulação no Cisco Packet Tracer

Os arquivos relacionados à simulação estão disponíveis em:

[Ver projeto do Cisco Packet Tracer](packet-tracer/)

A simulação foi utilizada para representar a topologia, os roteadores, as redes locais, os servidores e os clientes antes da implementação no VirtualBox.

## Site do projeto

A documentação visual do projeto está publicada no GitHub Pages:

[🌐 Acessar o site do projeto](https://gustavobarretomp.github.io/virtualized-network-scenario-1/)

## Testes realizados

Durante a implementação, foram executados testes como:

```bash
ping -c 4 192.168.1.10
```

```bash
curl http://192.168.1.10
```

```bash
nslookup servidor1.rede.local 192.168.1.5
```

```bash
nslookup servidor3.rede.local 192.168.4.5
```

```bash
sudo vtysh -c "show ip route"
```

```bash
sudo vtysh -c "show ip rip"
```

## Resultados

Os testes comprovaram:

- funcionamento do roteamento dinâmico RIPv2;
- aprendizagem de rotas entre os cinco roteadores;
- comunicação entre as cinco redes locais;
- funcionamento dos enlaces ponto a ponto;
- resolução dos nomes da zona `rede.local`;
- funcionamento dos servidores BIND9;
- funcionamento dos três servidores Apache2;
- acesso HTTP entre clientes e servidores de redes diferentes;
- funcionamento das redes internas utilizadas como switches virtuais no VirtualBox.

## Conhecimentos aplicados

Durante o desenvolvimento foram aplicados conhecimentos de:

- endereçamento IPv4;
- subnetting;
- roteamento dinâmico;
- administração de sistemas Linux;
- configuração de interfaces com Netplan;
- resolução DNS;
- servidores HTTP;
- virtualização;
- testes e diagnóstico de redes;
- documentação técnica com GitHub.

## Autor

**Gustavo Barreto**

Projeto desenvolvido para estudo e prática de redes de computadores, virtualização e segurança da informação.
