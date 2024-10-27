# Automated SAST/DAST in CI/CD Pipelines with Bearer

Este repositório configura um pipeline de Integração Contínua (CI) automatizado para realizar análises de segurança em tempo de desenvolvimento, utilizando o **Bearer** para análise estática de segurança de aplicações (SAST). Esse pipeline é especialmente útil para detectar vulnerabilidades e falhas de conformidade de privacidade e segurança desde as fases iniciais do ciclo de desenvolvimento, mapeando fluxos de dados confidenciais para detectar Informações de Identificação Pessoal (PII).

## Objetivo

O objetivo deste projeto é oferecer um pipeline completo para:
- Identificação e mitigação de vulnerabilidades no código-fonte através de análise estática (SAST).
- Detecção de dados sensíveis e práticas que possam violar a privacidade.
- Criação de relatórios automáticos que ajudam a identificar e priorizar riscos de segurança.

## Pré-requisitos

- **Bearer CLI**: O Bearer CLI precisa estar instalado na máquina de CI/CD.
- ### Instalação para Sistemas Linux:
  - Para instalar o Bearer CLI, execute:
    ```bash
    curl -sfL https://raw.githubusercontent.com/Bearer/bearer/main/contrib/install.sh | sh
    ```
  - Para sistemas baseados em Debian/Ubuntu:
    ```bash
    sudo apt update && sudo apt install bearer
    ```
- ### Instalação no Windows através do WSL com Kali Linux:
  Se você estiver utilizando o Windows com o WSL (Windows Subsystem for Linux) e tiver o Kali Linux configurado, siga os passos abaixo para instalar o Bearer:

  1. **Instale o WSL**:
     - Certifique-se de que o WSL está ativado no Windows. Abra o PowerShell como administrador e execute:
       ```powershell
       wsl --install
       ```
     - Reinicie o computador se necessário e instale a distribuição do Kali Linux pela Microsoft Store.

  2. **Abra o Kali Linux pelo WSL**:
     - Após a instalação, inicie o terminal do Kali Linux e atualize os pacotes com o comando:
       ```bash
       sudo apt update && sudo apt upgrade
       ```

  3. **Instale o Bearer no Kali Linux (WSL)**:
     - Execute o comando de instalação abaixo diretamente no terminal do Kali Linux:
       ```bash
       curl -sfL https://raw.githubusercontent.com/Bearer/bearer/main/contrib/install.sh | sh
       ```
       Após seguir esses passos, o Bearer estará instalado no WSL e pronto para ser utilizado dentro do ambiente do Kali Linux.

## Configuração do Bearer

1. **Clone o Repositório**:
   - Clone este repositório para seu ambiente local ou de CI/CD:
     ```bash
     git clone https://github.com/had-nu/Automated-SAST-DAST-CI-Pipeline-w-Bearer.git
     ```

2. **Executando o Bearer Localmente**:
   - No diretório do projeto, você pode executar o Bearer CLI para um teste local:
     ```bash
     bearer scan caminho-do-projeto
     ```
   - Isso gerará um relatório com detalhes de segurança, onde você poderá verificar problemas como dados sensíveis ou práticas de programação inseguras.

## Integração com o Pipeline CI/CD

1. **Configuração do Pipeline**:
   - No arquivo de configuração do pipeline (ex: `.yaml` para o Azure DevOps), adicione o seguinte comando para integrar o Bearer ao pipeline de CI/CD:
     ```yaml
     - script: bearer scan caminho-do-projeto
       displayName: 'Execução do Bearer SAST'
     ```
   - Esse comando rodará o Bearer automaticamente sempre que o pipeline for executado, gerando um relatório ao final do processo.

2. **Personalização das Regras**:
   - O Bearer permite que você configure regras customizadas para adaptar a análise de acordo com as necessidades de segurança específicas do projeto. Para isso, consulte a [documentação oficial do Bearer](https://docs.bearer.com) para definir regras adicionais.

## Resultados e Relatórios

Após cada execução, o Bearer gera um relatório detalhado com:
- Lista de vulnerabilidades identificadas, incluindo descrição, criticidade e localização no código.
- Alertas sobre dados sensíveis detectados (como PII) e práticas que possam violar regulamentos de privacidade, como o GDPR.
- Sugestões para resolver os problemas identificados.

Os resultados ajudam a priorizar correções e mitigação de riscos antes da implantação.

## FAQ

1. **Quais linguagens o Bearer suporta?**
   - Bearer suporta uma variedade de linguagens de programação populares. Consulte a documentação para a lista completa de suporte.

2. **Posso rodar o Bearer em Docker?**
   - Sim, você pode usar o Bearer em Docker, facilitando sua execução em ambientes de CI/CD baseados em container.

3. **Como configuro alertas personalizados?**
   - Para configurar alertas específicos, adicione regras personalizadas no Bearer para ajustar as verificações e tornar a análise mais relevante para seu projeto.

---

Para mais informações sobre o Bearer e seu uso, acesse a [documentação oficial do Bearer](https://docs.bearer.com).


## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

