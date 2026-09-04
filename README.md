# Folha Norte

Uma folha para definir a tua direção a um ano e revê-la **uma vez por mês — nem antes, nem depois**.

App estática (HTML/CSS/JS, sem build), instalável como PWA. Os dados ficam só no teu
dispositivo (`localStorage`). Publicável de graça no GitHub Pages.

## O método

1. **Onde estou agora** e **onde quero chegar** (a projeção). O horizonte é à tua
   escolha — dias, semanas, meses ou anos — e a app mostra a data-alvo.
2. **O que preciso de reunir** — informações, conteúdos e conhecimentos concretos.
3. **Compromisso** com a direção apontada.
4. **Revisão mensal** num dia fixo (sugestão: dia 22). Fora desse dia a folha está
   fechada — é a *blindagem* contra a procrastinação e a fuga.

A app acrescenta ao método:
- **Desbloqueio de emergência** — para um facto novo real (não "mudei de ideias"),
  com justificação obrigatória que fica no histórico.
- **Histórico** de traçado, revisões, reflexões e desbloqueios.
- **Exportar / importar** a folha em ficheiro (backup e portabilidade).
- **Imprimir** — gera a folha A4 fiel ao método (que pede papel).

## Correr localmente

Abre `index.html` no browser. Para o service worker (PWA) funcionar precisas de
`http://localhost`:

```
npx serve .
```

## Ícones do PWA

Abre `icons/generate.html` uma vez num browser, descarrega `icon-192.png` e
`icon-512.png` e coloca-os em `icons/`.

## Deploy (GitHub Pages)

`git push` para `main` → Pages publica em ~2 min. Sem CI.

## Línguas

`i18n.js` tem `pt` (Portugal) e `en`. Acrescentar uma língua = mais uma chave de
topo com o mesmo conjunto de campos.

## Próximos passos (fora da v1)

- Contas + sincronização na nuvem (Supabase) — permite multi-user.
- Assistente de IA (sugerir conhecimentos, questionar coerência) — implica chave de
  API, Termos & Condições e aviso do AI Act.
- Planos pagos / checkout (Stripe / referência `pt-checkout-builder`).
