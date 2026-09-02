# Projeto Aplicado: Infraestrutura Cloud & Observabilidade SRE

**Instituição:** Campus da Universidade Estadual de Ciências da Saúde de Alagoas - UNCISAL  
**Curso:** Segurança da Informação e Análise Forense  
**Matéria:** Projeto Aplicado: Práticas de Mercado  
**Professor:** Ziraldo Aurélio Cardoso de Oliveira  

**Aluno:** Adelson Eleotério Siqueira dos Santos  
**Matrícula:** 20252ESPSIAF0001

Repositório oficial para a arquitetura de alta disponibilidade e segurança baseada no conceito *Secure by Design*, desenvolvida em instâncias Oracle Cloud (Free Tier).

## 🛠️ Arquitetura
- **Eixo 1 (Infraestrutura)**: VM001 (Aplicação & Web Server): Hospeda o Nginx com HTTPS, Fail2Ban ativado para proteção SSH (4 tentativas / 24h) e Promtail para coleta de logs. VM002 (Central de Observabilidade): Centraliza as métricas e logs via Prometheus, Loki e Grafana.
- **Eixo 2 (Versionamento)**: Código versionado no GitHub com regras restritas no `.gitignore` para proteção de dados sensíveis.
- **Eixo 3 (Aplicação Segura)**: Protótipo web contendo tela de login, painel interno e botão de logout funcional.

---

## 🛡️ Mitigações OWASP Top 10 Implementadas

O projeto implementa defesas ativas contra vetores críticos listados no OWASP Top 10:

1. **A01:2025 - Broken Access Control (Controle de Acesso Quebrado)**:
   - *Onde se aplica*: Na verificação de sessão implementada via script no `dashboard.html`.
   - *Como mitigar*: O acesso à página interna exige validação prévia do estado de autenticação armazenado (`sessionStorage`), redirecionando imediatamente usuários não autorizados para a tela de login.

2. **A07:2025 - Identification and Authentication Failures (Falhas de Identificação e Autenticação)**:
   - *Onde se aplica*: Nos fluxos de entrada (`index.html`) e saída (`dashboard.html`).
   - *Como mitigar*: O sistema exige o preenchimento estrito de credenciais válidas e limpa o escopo de sessão de forma segura ao acionar o botão de logout, além da proteção perimetral na VM com Fail2Ban contra ataques de força bruta na porta SSH.

3. **A05:2025 - Security Misconfiguration (Inconfiguração de Segurança)**:
   - *Onde se aplica*: Na arquitetura de rede e publicação dos serviços.
   - *Como mitigar*: Isolamento rígido de portas de backend de observabilidade, uso de HTTPS com Certbot no Nginx com redirecionamento forçado, e ausência total de credenciais hardcoded no repositório.