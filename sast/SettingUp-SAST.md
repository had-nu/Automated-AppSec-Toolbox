# Configurando SAST

## Sobre o Bearer
Bearer CLI é uma ferramenta de Teste Estático de Segurança de Aplicações (SAST) que escaneia seu código-fonte e analisa seus fluxos de dados para descobrir, filtrar e priorizar riscos de segurança e privacidade.

Atualmente com suporte para: JavaScript/TypeScript, Ruby, PHP, Java, Go, Python

O Bearer CLI verifica seu código-fonte em busca de riscos de segurança e vulnerabilidades usando [regras integradas](https://docs.bearer.com/reference/rules/) que abrangem o [OWASP Top 10](https://owasp.org/www-project-top-ten/) e o [CWE Top 25](https://cwe.mitre.org/top25/archive/2023/2023_top25_list.html).

O Bearer CLI também verifica seu código-fonte em busca de riscos de privacidade com a capacidade de detectar [fluxo de dados sensíveis](https://docs.bearer.com/explanations/discovery-and-classification/), como o uso de PII, PHI em sua aplicação e [componentes](https://docs.bearer.com/reference/recipes/) que processam dados sensíveis (por exemplo, bancos de dados como pgSQL, APIs de terceiros como OpenAI, Sentry, etc.) que ajudam a gerar [relatórios de privacidade](https://docs.bearer.com/guides/privacy/).

Se quiser saber mais sobre a ferramenta, consulte a [documentação oficial](https://docs.bearer.com/).

### Configurando o Bearer
O *Bearer CLI* está disponível como um *Docker image* no [Docker Hub](https://hub.docker.com/r/bearer/bearer) e [ghcr.io](https://github.com/bearer/bearer/internals/container/bearer).

### Verificando um projeto
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

### Resultados e Relatórios
Após cada execução, o Bearer gera um relatório detalhado com:
- Lista de vulnerabilidades identificadas, incluindo descrição, criticidade e localização no código.
- Alertas sobre dados sensíveis detectados e práticas que possam violar regulamentos de privacidade, como o GDPR.
- Sugestões para resolver os problemas identificados.

Os resultados ajudam a priorizar correções e mitigação de riscos antes da implantação.

---

## Sobre o OWASP Juice Shop
O OWASP Juice Shop simula um aplicativo JavaScript realista com falhas de segurança comuns. É a maneira mais fácil de experimentar o Bearer CLI.

> Você pode encontrar algumas variações de instalação menos comuns, bem como instruções para executar o Juice Shop em uma variedade de provedores de computação em nuvem em [the *Running OWASP Juice Shop* documentation](https://pwning.owasp-juice.shop/companion-guide/latest/part1/running.html).

### Configurando Juice Shop
**From Sources**
  1. Instale [node.js](https://github.com/juice-shop/juice-shop?tab=readme-ov-file#nodejs-version-compatibility)
  2. Execute o comando `git clone https://github.com/juice-shop/juice-shop.git --depth 1` (ou
  clone [seu próprio fork](https://github.com/juice-shop/juice-shop/fork) do repositório)
  3. Use o comando `cd juice-shop` para ir até o diretório clonado localmente
  4. Execute o comando `npm install` (só precisa ser feito antes da primeira inicialização ou quando você altera o código-fonte)
  5. Execute o comando `npm start`
  6. Em seu navegador, acesse [http://localhost:3000](http://localhost:3000/)

    
**Docker Container**
  1. Instale o [Docker](https://www.docker.com/)
  2. Execute o comando `docker pull bkimminich/juice-shop`
  3. Execute o comando `docker run --rm -p 127.0.0.1:3000:3000 bkimminich/juice-shop`
  4. Em seu navegador, acesse http://localhost:3000/#/ (no macOS e no Windows acesse
  [http://192.168.99.100:3000](http://192.168.99.100:3000/) se você estiver usando docker-machine em vez da instalação nativa do Docker)

---

**Troubleshooting**

  Se precisar de ajuda com a configuração da aplicação, consulte o [Guia de Solução de Problemas do OWASP Juice Shop](https://pwning.owasp-juice.shop/appendix/troubleshooting.html).
  Se isso não resolver o seu problema, publique-o no [Gitter Chat](https://gitter.im/bkimminich/juice-shop) onde os membros da comunidade podem tentar ajudá-lo melhor.

  ---

### Verificando o Juice Shop

Uma vez que você clonou ou baixou o OWASP Juice Shop, agora você pode executar o comando scan com bearer scan no diretório do projeto

```
bearer scan juice-shop
```
Uma barra de progresso exibirá o status da varredura.

Assim que a varredura for concluída, o Bearer CLI emitirá, por padrão, um relatório de segurança com detalhes de quaisquer descobertas de regras, bem como onde na base de código as infrações aconteceram e por quê.

Por padrão, o comando `scan` usa a varredura SAST, entretanto outros [tipos de varredura](https://docs.bearer.com/explanations/scanners) estão disponíveis.

### Analisando os Relatórios

O relatório de segurança é uma visão facilmente digerível dos problemas de segurança detectados pelo Bearer CLI. Um relatório é composto por:

- A lista de [regras](https://docs.bearer.com/reference/rules/) executadas em seu código.
- Cada descoberta detectada, contendo o local do arquivo e as linhas que acionaram a descoberta da regra.
- Uma seção de estatísticas com um resumo das verificações de regras, descobertas e avisos.

O OWASP Juice Shop acionará descobertas de regras e produzirá um relatório completo. Eis um exemplo de uma seção da saída:

```
...
HIGH: Sensitive data stored in HTML local storage detected. [CWE-312]
https://docs.bearer.com/reference/rules/javascript_lang_session
To skip this rule, use the flag --skip-rule=javascript_lang_session

File: juice-shop/frontend/src/app/login/login.component.ts:102

 102       localStorage.setItem('email', this.user.email)


=====================================

59 checks, 40 findings

CRITICAL: 0
HIGH: 16 (CWE-22, CWE-312, CWE-798, CWE-89)
MEDIUM: 24 (CWE-327, CWE-548, CWE-79)
LOW: 0
WARNING: 0
```
Além do relatório de segurança, você também pode executar um [relatório de privacidade](https://docs.bearer.com/explanations/reports/#privacy-report).

Opções adicionais para usar e configurar o comando `scan` podem ser encontradas em [configurando o comando scan](https://docs.bearer.com/guides/configure-scan/).