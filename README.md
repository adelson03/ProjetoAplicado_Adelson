# Projeto Aplicado - Infraestrutura Cloud & Observabilidade SRE

Repositório oficial para a arquitetura de alta disponibilidade e segurança baseada no conceito *Secure by Design*, desenvolvida em instâncias Oracle Cloud (Free Tier).

## Arquitetura
- **VM001 (Aplicação & Web Server):** Hospeda o Nginx com HTTPS, Fail2Ban ativado para proteção SSH (4 tentativas / 24h) e Promtail para coleta de logs.
- **VM002 (Central de Observabilidade):** Centraliza as métricas e logs via Prometheus, Loki e Grafana.

## Requisitos OWASP Implementados
- Controle de sessão seguro utilizando `sessionStorage` para evitar persistência indevida de tokens.
- Sanitização básica de entradas na tela de autenticação.
- Proteção contra força bruta no nível do sistema operacional (Fail2Ban).