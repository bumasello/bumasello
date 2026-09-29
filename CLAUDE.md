# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## O que este repositório é

Não há código. O repo é `bumasello/bumasello` — nome igual ao do usuário do
GitHub, o que faz dele o **profile README especial**: o `README.md` da raiz é
renderizado no topo de <https://github.com/bumasello>.

- Único arquivo versionado além deste: `README.md`. Sem build, teste, lint, CI.
- Publicar = `git push` na `main`. O GitHub renderiza direto, não há deploy.
- É uma landing page cujo público é recrutador. O Bruno está empregado e
  procurando (set/2026), então o texto é material de candidatura, não enfeite.

## A regra que governa o conteúdo

O README foi reescrito em 28/09/2026 para aplicar ao perfil a mesma regra do
mazetick: **nenhum número sobe sem a fonte junto**. Antes disso ele tinha cinco
métricas sem origem ("+1TB mensalmente", "30% de redução", "15+ automações",
"40+ horas/semana", "5+ departamentos") e duas competências que contradizem o
registro verificado dele. Isso é o defeito a não reintroduzir.

Consequência prática: **nenhum número, data ou tecnologia entra aqui sem sair de
uma das fontes abaixo.** Se a fonte não tem, o número não entra.

## Onde ficam os fatos

| fonte | o que ela decide |
|---|---|
| `~/dev/claude/ai-job-search/.claude/skills/job-application-assistant/01-candidate-profile.md` | **a fonte canônica.** Experiência, stack, projetos, e os limites de honestidade |
| `~/dev/claude/ai-job-search/cv/main_general.txt` | o CV em inglês, para datas e títulos de cargo |
| `~/dev/node/mazetick/src/content/research/*.md` | os números de turfe. O frontmatter traz `sample`, `window`, `method`, `derivation` (script@commit) e `measured` |
| `~/dev/node/mazetick/README.md` | **a amostra da voz dele em inglês.** É o que a `humanizer` precisa receber |
| vault, `30-referencias/catalogo-50-claude-skills.md` | o que está instalado e por quê |

O `01-candidate-profile.md` marca vários fatos com `(confirmed by candidate
<data>)`. Esses são checados com ele; não contradiga sem perguntar.

## Limites de honestidade — não reintroduzir

O `01-candidate-profile.md` lista o que **não** pode ser afirmado. Os que já
foram violados uma vez pelo README antigo:

- **Sem experiência profissional de teste automatizado.** Teste unitário só em
  projeto de estudo. O README antigo listava "Teste de Unidade" como competência.
- **Machine Learning**: ele integrou modelos no trabalho, mas a conclusão medida
  do mazetick é que ML *não* bateu o mercado. Citar como competência isolada
  contradiz o que ele publicou.
- **CI/CD só em projeto pessoal** (GitHub Actions). Nunca profissionalmente,
  e Jenkins nunca.
- **Sem code review profissional** — o empregador não pratica.
- **Nunca configurou servidor MCP.** O que ele tem é function calling do Gemini.
- **Nada de n8n, Zapier, Make.** A automação dele é escrita em código.
- **Sem C# nem Unity ainda** (estudando C#, motivado por gamedev).
- **Inglês fluente, mas ele não trabalha em inglês no dia a dia** — a Rede D'Or
  opera em português.
- O repo `appQualidade` é **trabalho do empregador**: descrever o app, nunca
  citar a URL do repo.

A seção "What I have not done" existe justamente para deixar isso na página, o
que é escolha deliberada e não descuido a corrigir.

## Voz e forma

Inglês, decidido em 28/09/2026 — o CV, o mazetick e os READMEs dos repos dele já
são em inglês, e o alvo inclui remoto internacional.

A identidade escolhida é **registro, no espírito do mazetick**: a distinção vem
da página *se comportar* como registro (número com fonte, data, amostra, os
fracassos publicados), não de ornamento. Ver no vault
`o-mazetick-e-um-diario-oficial-do-mercado-nao-um-jornal`.

Portanto:

- **Zero badge do shields.io, zero cartão de stats, zero contador de views.**
  O render atual tem **0 tags `<img>`** e nenhuma dependência de terceiro. Era a
  parede de ~25 imagens que fazia o perfil parecer gerado. Não devolver.
- **Sem `<div align="center">`** e sem régua horizontal entre seções — o `##` do
  GitHub já desenha a sua.
- **Nenhum travessão** (`—` ou `–`). A §8 da `humanizer` manda trocar por ponto,
  vírgula, dois-pontos ou parênteses, e a exceção que permitiria manter a taxa do
  autor exige uma amostra da escrita dele — o README do mazetick ainda vai passar
  pela `humanizer`, então não serve de amostra. Hífen de palavra composta e o
  sinal de menos `−` dos percentuais negativos ficam.
- O diagrama é mermaid, **nativo do GitHub** — não carregar biblioteca.

## Como validar sem publicar

Não existe preview local do GitHub, mas dá para renderizar com a API dele e
fotografar o resultado, sem `push`:

```bash
# 1. renderiza o markdown como o GitHub renderiza
python3 -c "import json;json.dump({'text':open('README.md').read(),'mode':'gfm','context':'bumasello/bumasello'},open('/tmp/md.json','w'))"
gh api -X POST /markdown --input /tmp/md.json > /tmp/rendered.html

# 2. confere o que saiu (img deve ser 0)
grep -oE '<img|<script|lang="mermaid"' /tmp/rendered.html | sort | uniq -c
```

Para a foto, embrulhe o fragmento em `github-markdown-css`, converta
`<pre lang="mermaid">` em `<pre class="mermaid">`, rode o mermaid do CDN e tire
screenshot com Playwright em `color_scheme` light e dark. O módulo Python não
está instalado, mas os browsers estão em `~/.cache/ms-playwright`, então
`uv run --with playwright python <script>` resolve sem sujar nada.

O `Loading` que aparece sob o diagrama no HTML da API é o placeholder do próprio
GitHub para render client-side. É sinal de que o mermaid vai desenhar, não erro.

## Skills que valem aqui

`humanizer` (passe o README do mazetick como amostra), `copywriting` e
`copy-editing` (público recrutador), `webapp-testing` (a validação acima),
`segundo-cerebro`. Instaladas em 28/09/2026 junto com `find-skills` e
`algorithmic-art`.

Não servem, apesar de parecerem: `frontend-design`, `theme-factory` e afins
pedem CSS, que não existe em markdown do GitHub; `img-to-html` recria mock como
HTML e não valida nada.
