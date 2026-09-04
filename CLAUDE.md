# Folha Norte — instruções para o Claude

App estática (HTML/CSS/JS, sem build, sem framework, sem servidor) que implementa o
método "Folha Norte": planeamento pessoal a 1 ano com revisão mensal num dia fixo.
Publicável no GitHub Pages. Dados só no dispositivo (`localStorage`).

## Ficheiros

| Ficheiro | Papel |
|---|---|
| `index.html` | Estrutura. Dois estados: `#view-empty` (sem folha) e `#view-folha`. |
| `app.js` | Toda a lógica. IIFE, `localStorage`, blindagem, histórico, export/import. |
| `i18n.js` | `window.I18N.{pt,en}`. Acrescentar língua = nova chave de topo completa. |
| `styles.css` | Design "instrumento de navegação": banda com bússola + folha A4. |
| `sw.js` / `manifest.json` | PWA. App shell offline. |
| `icons/generate.html` | Gera os PNG dos ícones (correr uma vez no browser). |

## Estado (localStorage)

- `fn.folha` — `{ createdAt, horizon, projecao, atual, needs[], commit, nome, history[] }`
  - `horizon` — `{ n, unit: "day"|"week"|"month"|"year" }`. A data-alvo é calculada
    a partir de `createdAt` (ver `addHorizon()`), não guardada. Folhas importadas
    sem `horizon` assumem `{ n: 1, unit: "year" }`.
- `fn.config` — `{ reviewDay }` (1–28)
- `fn.lang` — `"pt"` | `"en"`

`needs[]` = `{ id, type: "informacao"|"conteudo"|"conhecimento", desc, done }`
`history[]` = `{ at, type: "created"|"review"|"reflection"|"emergency", text }`

## Blindagem — não enfraquecer sem o Nando confirmar

É o núcleo do método, não um detalhe de UI:
- Fora do `reviewDay` os campos do plano ficam `disabled` (ver `renderLock()`).
- No `reviewDay` a folha abre e guardar exige uma nota de revisão (`#dlg-review`).
- Sempre disponível: registar reflexão (append-only, não altera o plano).
- Desbloqueio de emergência: exige justificação (≥40 caz.), regista `emergency` no
  histórico, dura só a sessão, fecha ao guardar.

Não adicionar "editar sempre", nem remover o diálogo de revisão, nem alargar a
janela de edição para além do próprio dia.

## Segurança

- Nunca introduzir chamadas de rede em uso normal. A app é 100% offline.
- Sem tokens, sem chaves. Se algum dia entrar IA/nuvem, é backend separado (padrão
  `Task.Talk` / Cloudflare Worker do `Dashboard do Dinis`), nunca segredos no cliente.

## Fluxo de trabalho

Ficheiro único por área — ao pedir alterações, devolver o(s) ficheiro(s) completo(s).
Testar abrindo `index.html` ou `npx serve .`.
