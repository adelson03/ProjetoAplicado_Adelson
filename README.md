# Projeto Aplicado: Práticas de Mercado
**Curso:** Segurança da Informação e Análise Forense  
**Instituição:** Universidade Estadual de Ciências da Saúde de Alagoas (UNCISAL)  
**Professor:** Ziraldo Aurélio Cardoso de Oliveira  
**Aluno/Desenvolvedor:** Adelson Eleotério Siqueira dos Santos (Matrícula: 20252ESPSIAF0001)  

---

## 📋 Sobre o Projeto
Este repositório contém o desenvolvimento da interface web segura, painel administrativo e a infraestrutura de suporte (Eixos de desenvolvimento e infraestrutura) do Projeto Aplicado. O sistema contempla mecanismos de autenticação restrita, controle de sessão via `sessionStorage`, identidade visual institucional padronizada, arquitetura em nuvem distribuída, observabilidade avançada e automação de entrega contínua (CI/CD).

---

## 🛠️ Tecnologias e Ferramentas Utilizadas
* **Frontend:** HTML5, CSS3, JavaScript (Vanilla).
* **Controle de Versão:** Git e GitHub.
* **Infraestrutura & Cloud (OCI):** Oracle Cloud Infrastructure - Instâncias Dedicadas (`VM001` e `VM002`).
* **Hardware das Instâncias:** VM.Standard.E2.1.Micro (1 OCPU, 1 GB RAM).
* **Sistema Operacional:** Ubuntu Linux.
* **Observabilidade e Monitoramento:** Prometheus, Grafana e Loki.
* **Automação (CI/CD):** GitHub Actions e SSH Deployment.
* **Servidor Web:** Nginx.

---

## ☁️ Arquitetura de Servidores na OCI (Oracle Cloud Infrastructure)
A infraestrutura em nuvem do projeto foi dimensionada em instâncias separadas executando **Ubuntu Linux** (Shape `VM.Standard.E2.1.Micro` com 1 OCPU e 

1 GB de RAM) para isolar as camadas de aplicação e monitoramento:
1. **ProjetoVM001 (Produção / Aplicação Web):**
   * **IP Público:** `167.234.236.107`
   * **Hardware:** 1 OCPU / 1 GB RAM (`VM.Standard.E2.1.Micro`)
   * **Sistema Operacional:** Ubuntu Linux
   * **Função:** Hospedagem da aplicação web principal, tela de login, painel administrativo e servidor web Nginx.

2. **ProjetoVM002 (Observabilidade e Monitoramento):**
   * **IP Público:** `163.176.142.188`
   * **Hardware:** 1 OCPU / 1 GB RAM (`VM.Standard.E2.1.Micro`)
   * **Sistema Operacional:** Ubuntu Linux
   * **Função:** Ambiente dedicado à observabilidade e métricas de infraestrutura.
   * **Stack Tecnológica:** 
     * **Prometheus:** Coleta e armazenamento de métricas de desempenho e integridade dos sistemas.
     * **Grafana:** Visualização de dados, criação de dashboards analíticos e alertas operacionais.
     * **Loki:** Sistema de agregação e consulta centralizada de logs dos serviços.

---

## 🚀 Estrutura do Sistema Web
O projeto web é composto por duas telas principais que gerenciam o fluxo de acesso restrito:
1. **`index.html` (Tela de Login):** Interface contendo validação de campos obrigatórios, suporte ao evento de submissão via tecla `Enter` e integração com a identidade visual da UNCISAL.
2. **`dashboard.html` (Painel Administrativo):** Área restrita protegida por validação de sessão, exibindo dados institucionais, informações do discente, logotipo oficial e botão seguro de encerramento de sessão (Logout).

---

## ⚙️ Configuração e Execução Local
Caso deseje executar o projeto localmente para fins de teste:
1. Clone o repositório em sua máquina:
   ```bash
   git clone [https://github.com/adelson03/ProjetoAplicado_Adelson.git](https://github.com/adelson03/ProjetoAplicado_Adelson.git)

---

## 🛡️ Mitigação de Falhas (OWASP Top 10)

Em conformidade com os requisitos do Projeto Aplicado, foram documentadas e mitigadas as seguintes vulnerabilidades do **OWASP Top 10**:

1. **A01:2021 – Broken Access Control (Controle de Acesso Quebrado):**
   * **Mitigação:** Implementada validação restrita de sessão via `sessionStorage` no painel administrativo (`dashboard.html`), impedindo o acesso direto às telas restritas sem passar pelo fluxo legítimo de autenticação do `index.html`.
2. **A03:2021 – Injection (Injeção):**
   * **Mitigação:** Aplicação de validação rigorosa de entradas de formulário e tratamento adequado de caracteres nos campos de autenticação.
3. **A05:2021 – Security Misconfiguration (Configuração Incorreta de Segurança):**
   * **Mitigação:** Endurecimento (*hardening*) do servidor web Nginx, desativação de assinaturas de versão e imposição de cabeçalhos de segurança TLS/SSL.

