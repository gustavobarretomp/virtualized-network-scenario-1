# Cenário 01 — Rede Virtualizada com RIPv2, DNS e HTTP

Projeto de implementação de uma infraestrutura de rede virtualizada utilizando cinco roteadores, cinco redes locais, servidores DNS, servidores web e clientes de teste.

O ambiente foi construído inicialmente no Cisco Packet Tracer e depois implementado no Oracle VirtualBox com máquinas Ubuntu Server.

## Objetivos

- configurar o roteamento dinâmico com RIPv2;
- permitir a comunicação entre diferentes redes locais;
- implementar resolução de nomes com BIND9;
- disponibilizar páginas HTTP com Apache2;
- validar a infraestrutura por meio de testes de conectividade, DNS e HTTP.

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

## Estrutura do projeto

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
