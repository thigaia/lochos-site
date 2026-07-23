# Lochos — Site

Site institucional do Lochos (landing page + páginas legais). Estático, sem build: HTML + CSS + um JS pequeno, servido direto.

## Domínio e deploy

- **Domínio:** `lochos.com.br` (arquivo [`CNAME`](CNAME))
- **Hospedagem:** GitHub Pages (o `CNAME` na raiz é a convenção do Pages para domínio próprio)
- **DNS:** o domínio aponta para o Pages via registro DNS no provedor do domínio. Depois de alterar DNS, a propagação pode levar de alguns minutos a algumas horas — se o site não abrir logo após uma mudança de DNS, geralmente é só aguardar propagar (checar com `nslookup lochos.com.br` ou dnschecker.org).
- **Status:** site no ar com **HTTPS** e **GA4** (`G-3VPJLFXJB4`); Search Console + Bing configurados.

## Estrutura

```
lochos-site/
├── index.html          → landing page (hero, como funciona, recursos, planos, FAQ)
├── privacidade.html    → Política de Privacidade
├── termos.html         → Termos de Uso
├── exclusao-de-conta.html → Página de exclusão de conta (usada no Play Console)
├── (5 páginas de conteúdo / guias)  → SEO — intenção aguda (Persona A) + prevenção (Persona B)
├── CNAME               → domínio do GitHub Pages (lochos.com.br)
└── assets/
    ├── styles.css      → estilos (design tokens espelham o app: fundo #0A0A0A, dourado premium, etc.)
    ├── app.js          → interações leves (header ao rolar, acordeão do FAQ, ano no rodapé)
    ├── capybara-white.png
    └── logo-mark.png
```

## Como atualizar

1. Editar os `.html` / `assets/` direto.
2. As páginas legais têm a data em `Última atualização:` no topo — atualizar quando o conteúdo mudar de fato.
3. Publicar (commit/push pro branch que o Pages serve, ou o fluxo de deploy em uso).

## Consistência com o conteúdo do app

O texto do site deve bater com o comportamento real do app:

- A verificação da palavra-chave **exige internet** (transcrição na nuvem via Supabase Edge Function + OpenAI) — o FAQ diz isso explicitamente. **Não** afirmar que funciona offline.
- A política de privacidade cita os terceiros reais: **OpenAI** (transcrição) e **Supabase** (registros). O áudio é enviado ao servidor para verificação e **não é armazenado** lá — e o **texto transcrito também não é retido** (usado só em memória pra detectar a palavra-chave e descartado; `voice_checks` não tem coluna `transcript`).
- Preços/planos: Premium R$ 29,90/mês (7 dias grátis), Familiar "Em breve". O Google Play Billing **já está integrado e validado ponta a ponta**; o download público segue "Em breve" porque falta o **teste fechado (≥12 testadores/≥14 dias)** antes de solicitar produção — não porque o billing não exista (ver `../Lochos App Android/PLANO_GOOGLE_PLAY_BILLING.md`).

Ver `../Lochos App Android/README.md` e `COMO_FUNCIONA.md` para a arquitetura do app.

## ⚠️ Cópia espelhada em `docs/` do app

Existe uma segunda cópia idêntica deste site em `../Lochos App Android/docs/` (index/privacidade/termos + assets). **Fonte da verdade é esta pasta (`lochos-site/`)** — a de `docs/` é um espelho. Ao editar aqui, sincronizar a cópia de `docs/` para não divergirem (ou, quando o deploy estiver consolidado num só lugar, remover a duplicata).
