## Setting Up SAST

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
