# Automated Application Security Toolbox

Este repositório contém uma série de ferramentas ingradas para realizar testes de segurança em tempo de desenvolvimento, utilizando um conjunto de ferramentas para Teste Estático de Segurança de Aplicações (SAST), Teste Dinêmico de Aplicações (DAST), Teste Interativo de Segurança de Aplicações (IAST) e testes de segurança para Infraestrutura como Código (IaC). 

Esse pipeline é especialmente útil para detectar vulnerabilidades e falhas de conformidade de privacidade e segurança ainda nas fases iniciais do ciclo de desenvolvimento, mapeando fluxos de dados confidenciais para detectar Informações de Identificação Pessoal (PII).

## Objetivo

O objetivo deste projeto é oferecer uma estrutura integrada e automatizada de verificação de segurança para auxiliar equipes de desenvolvimento e operações na identificação, mitigação e prevenção de vulnerabilidades de segurança ao longo do ciclo de vida de desenvolvimento de software (SDLC). Este pipeline possibilita que qualquer desenvolvedor ou equipe de DevOps execute uma bateria de testes de segurança de maneira simplificada e eficiente.

## Ferramentas Utilizadas

O pipeline utiliza uma combinação de ferramentas open-source e soluções de segurança de código para verificar a integridade e conformidade da aplicação.

- **SAST (Static Application Security Testing)**: [Bearer](https://www.bearer.com/) via [Docker](https://www.docker.com/) para análise estática de vulnerabilidades diretamente no código-fonte do [OWASP Juice Shop](https://github.com/juice-shop/juice-shop?tab=readme-ov-file).
- **DAST (Dynamic Application Security Testing)**: [OWASP ZAP](https://www.zaproxy.org/) para testes dinâmicos em uma aplicação em execução, identificando possíveis falhas de segurança. (em construção)
- **IAST (Interactive Application Security Testing)**: [Contrast Security Community Edition](https://www.contrastsecurity.com/) e [Hdiv](https://www.hdivsecurity.com/) para fornecer análise interativa durante a execução de testes, com insights em tempo real sobre vulnerabilidades. (aguardando)
- **IaC (Infrastructure as Code)**: [Terraform](https://www.terraform.io/), [Terraform Compliance](https://terraform-compliance.com/) e [TFLint](https://github.com/terraform-linters/tflint) para verificar e assegurar conformidade e segurança na infraestrutura de código.(em construção)

## Estrutura do Repositório

Este repositório está organizado em diferentes diretórios para cada tipo de verificação:

- `/sast`: Configurações e scripts para SAST usando Bearer e Docker.
- `/dast`: Scripts e configurações para DAST com OWASP ZAP.
- `/iast`: Configurações e instruções para IAST, com Contrast Security e Hdiv.
- `/iac`: Configurações e scripts para verificações de IaC com Terraform, Terraform Compliance e TFLint.
- `/docs`: Documentação complementar e informações de configuração para cada ferramenta.
- `.github/workflows`: Arquivos YAML de workflow para integração contínua (CI/CD) no GitHub Actions, automatizando as verificações de segurança.

## Requisitos

Antes de começar, certifique-se de ter os seguintes pré-requisitos:

- Conta no GitHub e acesso ao [GitHub Actions](https://github.com/features/actions).
- Docker instalado para execução dos contêineres das ferramentas de segurança.
- Acesso aos registros do Docker para cada ferramenta configurada, se aplicável.
- Configurações de API e tokens de autenticação para Contrast Security e outras ferramentas, conforme necessário.
- Conta no Azure DevOps e acesso ao Azure Repos Git para sincronizar e versionar o código do projeto em pipelines de CI/CD, se aplicável.
- Configuração dos agentes de build do Azure DevOps para permitir a execução dos contêineres Docker e ferramentas de análise de segurança, se aplicável.

## Setting Up
<!-- 
<details><summary><b>SAST</b></summary>

**Configurando o Bearer**

O *Bearer CLI* está disponível como um *Docker image* no [Docker Hub](https://hub.docker.com/r/bearer/bearer) e [ghcr.io](https://github.com/bearer/bearer/internals/container/bearer).

**Escaneando um projeto**

Com o Docker instalado, você pode executar o seguinte comando com os caminhos apropriados no lugar dos exemplos marcados `{}`.
```
docker run --rm -v {/path/to/repo}:/tmp/scan bearer/bearer:latest-amd64 scan /tmp/scan
```
Você também pode usar o *Docker Compose*. Adicione o seguinte ao seu arquivo `docker-compose.yml` e substitua os volumes pelos caminhos apropriados para seu projeto:
```
version: "3"services:
  bearer:
    platform: linux/amd64
    image: bearer/bearer:latest-amd64
    volumes:
      - /path/to/repo:/tmp/scan
```
Em seguida, execute o comando `docker compose run` para executar o Bearer CLI com quaisquer sinalizadores especificados. Por exemplo:
```
docker compose run bearer scan /tmp/scan --debug
```
As configurações do Docker acima sempre usarão a versão mais recente.

**Personalização das Regras**

O Bearer permite que você configure regras customizadas para adaptar a análise de acordo com as necessidades de segurança específicas do projeto. Para isso, consulte a [documentação oficial do Bearer](https://docs.bearer.com) para definir regras adicionais.

Para configurar alertas específicos, adicione regras personalizadas no Bearer para ajustar as verificações e tornar a análise mais relevante para seu projeto.

**Resultados e Relatórios**

Após cada execução, o Bearer gera um relatório detalhado com:
- Lista de vulnerabilidades identificadas, incluindo descrição, criticidade e localização no código.
- Alertas sobre dados sensíveis detectados e práticas que possam violar regulamentos de privacidade, como o GDPR.
- Sugestões para resolver os problemas identificados.

Os resultados ajudam a priorizar correções e mitigação de riscos antes da implantação.


</details>

---

<details><summary><b>DAST</b></summary>

</details>

---

<details><summary><b>IAST</b></summary>

</details>

---

<details><summary><b>IaC</b></summary>

</details>

---
-->
<!-- 
## Configuração do Azure DevOps para Integração

Para integrar este repositório ao Azure DevOps, siga os passos abaixo:

1. **Crie um Projeto no Azure DevOps**: 
   - Navegue para a sua conta do Azure DevOps e crie um novo projeto com o nome desejado.
   - Configure o repositório do projeto para se conectar ao repositório GitHub e, assim, sincronizar automaticamente as alterações.

2. **Configurar Azure Pipelines**:
   - Crie um pipeline de CI/CD no Azure DevOps que chame os workflows definidos nos arquivos YAML deste repositório, garantindo a execução das verificações de segurança automaticamente.
   - Adicione as variáveis de ambiente e os tokens de autenticação necessários no pipeline, conforme especificado no arquivo `.env`.

3. **Ajustar os Agentes de Build**:
   - Configure os agentes de build do Azure DevOps para suportar as ferramentas de segurança, como Docker e OWASP ZAP, e permita que rodem os testes especificados nos workflows de SAST, DAST, IAST e IaC.

4. **Configurar SonarCloud ou Ferramentas Alternativas**:
   - Caso deseje incluir o SonarCloud como parte do pipeline, integre-o ao projeto para realizar análises adicionais de qualidade de código e conformidade com boas práticas.
-->

## Suporte

Caso enfrente dificuldades durante a instalação ou configuração do pipeline, consulte a documentação disponível em `/docs` ou entre em contato com o administrador do projeto para obter suporte adicional.

## Como Executar
<!--
1. **Clone o Repositório**:
   ```bash
   git clone https://github.com/usuario/Automated-AppSec-Verify-CICD-Pipelines.git
   cd Automated-AppSec-Verify-CICD-Pipelines
2. **Configurar Variáveis de Ambiente**:
   Crie um arquivo `.env` na raiz do projeto com as credenciais necessárias para as ferramentas (exemplo em `/docs/env-example`).

3. **Executar o Pipeline de Segurança**: 
Use o GitHub Actions para disparar as execuções automatizadas ou configure os workflows manualmente com os comandos especificados em cada diretório.

4. **Verificar Resultados**: 
Os relatórios de cada ferramenta estarão disponíveis nos artefatos do GitHub Actions e poderão ser exportados para análise e documentação.

-->
## Contribuindo

Contribuições são bem-vindas! Este é um projeto em construção de um estudante, então seja legal. 
Por favor, siga as diretrizes no arquivo `CONTRIBUTING.md` para submeter issues ou pull requests.

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.


*Este README fornece uma visão geral do projeto, incluindo as ferramentas utilizadas, estrutura do repositório, requisitos, e instruções de execução, facilitando a compreensão para novos usuários e desenvolvedores interessados em contribuir com o projeto.*

