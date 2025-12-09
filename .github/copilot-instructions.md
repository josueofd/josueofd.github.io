<!-- Copilot instructions for coding agents: concise, repository-specific guidance -->
# Instruções rápidas para agentes de IA (Copilot)

- **Propósito**: Este repositório é um site estático (páginas HTML prontas). Modificações geralmente envolvem editar arquivos HTML/CSS/JS diretamente (ex.: `roadmap-ciberseguranca.html`).

- **Visão geral (big picture)**:
  - Projeto: site pessoal/roadmap de cibersegurança. Não há backend nem bundlers no repositório atual.
  - Principais artefatos: `roadmap-ciberseguranca.html` (página principal), `README.md` (meta).
  - Integrações externas visíveis: Google Fonts, Material Symbols, Tailwind via CDN e vários scripts inline que fazem manipulação de imagens e chamadas externas (ver `roadmap-ciberseguranca.html`).

- **Padrões e convenções específicos deste projeto**:
  - Layout e estilos: Tailwind via CDN com muitas classes utilitárias inline; manter a consistência usando as mesmas classes (ex.: `glass-panel`, `cyber-gradient-text`).
  - Scripts: grande parte do comportamento está incorporado em scripts inline no HTML; alterar scripts exige testar localmente no navegador.
  - Imagens: há um mecanismo complexo de pré-processamento e substituição de imagens (busca/geração) dentro de `roadmap-ciberseguranca.html`. Não modifique nomes de chaves no mapa `IMG_*_MAP` sem entender o fluxo.

- **Fluxo de dados e áreas sensíveis**:
  - Vários trechos JavaScript fazem fetch para domínios Google/externos e lidam com blobs/URLs geradas. Alterações podem impactar CORS e o carregamento de imagens.
  - Há manipulação de atributos DOM (ex.: substituição de `src`) e observers (`MutationObserver`, `ResizeObserver`). Teste em páginas com conteúdo dinâmico.

- **Workflows de desenvolvedor (como testar/preview)**:
  - Pré-requisito: nenhum build; basta servir arquivos estáticos.
  - Comando local rápido (na raiz do repositório):

```bash
# abrir servidor simples na porta 8000
python3 -m http.server 8000
# ou, se preferir Node (instale live-server)
npx live-server --port=8000
```

  - Abra `http://localhost:8000/roadmap-ciberseguranca.html` para verificar as alterações no navegador.

- **O que evitar**:
  - Não remover ou minificar os grandes scripts inline sem replicar seu propósito — eles controlam substituição de imagens, atribuições e comportamento visual.
  - Evitar quebrar referências externas (fonts, icons, endpoints `googleusercontent`), pois o layout e imagens dependem deles.

- **Como adicionar uma nova página**:
  - Criar um novo arquivo `.html` na raiz ou em subpasta, seguir a estrutura do `roadmap-ciberseguranca.html` (head com links para Tailwind/Fonts, estilo global e scripts necessários).
  - Atualizar links de navegação manualmente no `nav` se necessário.

- **Exemplos de alterações seguras**:
  - Atualizar textos, seções de conteúdo e classes Tailwind.
  - Trocar imagens estáticas cujo `src` seja URL simples (não geradas) — teste no navegador.

- **Commit e deploy**:
  - Fluxo comum: editar -> git add/commit -> push para `main` (repo `josueofd.github.io` usa GitHub Pages automaticamente para `main`).
  - Comandos úteis:

```bash
git add <arquivo>.html
git commit -m "Atualiza conteúdo da página X"
git push origin main
```

- **Arquivos-chave para referência rápida**:
  - `roadmap-ciberseguranca.html` — principal página, contém a maior parte do código (HTML/CSS/JS).
  - `README.md` — repositório mínimo (meta).

- **Perguntas que o agente deve fazer quando estiver em dúvida**:
  - "Esta mudança afetará o comportamento de substituição de imagens (maps `IMG_*_MAP`)?"
  - "Preciso alterar URLs externos/recursos de fonte/icones?" — confirmar antes de editar.

Se algo estiver incompleto ou você quiser que eu inclua exemplos de código para tarefas específicas (ex.: extrair scripts inline para arquivos separados, ou um `preview` mais avançado), diga qual opção prefere.
