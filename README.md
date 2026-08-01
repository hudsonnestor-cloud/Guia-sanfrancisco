# SF Um Mês — Guia North Beach

PWA offline com tudo que você precisa para um mês em San Francisco morando perto da Molinari, estudando no ELI e indo alguns dias ao escritório em Menlo Park.

Vanilla JS, sem build, sem dependências. Um arquivo HTML + service worker.

---

## O que tem dentro

| Aba | Conteúdo |
|---|---|
| **Chip** | Plano de conectividade: T-Mobile U.S. Pass passo a passo, cobertura da viagem, especificações, plano B e comparativo de operadoras. |
| **Comutar** | Trajeto passo a passo Molinari → escritório via Muni linha T + Caltrain + shuttle M3 gratuito, com diagrama de rota animado. Três opções comparadas por custo e tempo. Clipper, passe mensal, trajeto até o ELI e regras de sobrevivência no transporte. |
| **Cozinha** | 3 receitas de marmita (rendem 5 porções cada) + 4 jantas de 20 minutos. Estratégia de domingo. |
| **Compras** | Onde comprar (Trader Joe's e mercados de bairro) + duas listas com checkbox salvo no aparelho: compra de instalação e compra semanal. |
| **Passeios** | Pontos turísticos separados por esforço (a pé de casa / meia diária / dia inteiro), com como chegar, quando ir e por que vale. |
| **O Mês** | Plano de 4 semanas, dia a dia, com ritmo semanal padrão. |
| **Essenciais** | Endereços, farmácias, lavanderias, urgent care, números e apps. |

## As duas descobertas que definem o trajeto

**1. North Beach tem metrô.** A estação **Chinatown–Rose Pak** (943 Stockton St) fica a 8–10 min a pé da Molinari e é a ponta norte da **linha T do Muni Metro**, que vai direto até a estação Caltrain de **4th & King**. Como é estação terminal, o trem sempre parte dali — você senta.

**2. A última perna é grátis.** O **M3–Marsh Road Shuttle**, da prefeitura de Menlo Park em parceria com a SamTrans, é gratuito, aberto a qualquer pessoa, e tem uma parada em **Bohannon Dr & Campbell Ave** — a esquina do escritório. Roda de segunda a sexta, aproximadamente das 7h45 às 17h35, com horários casados com a chegada dos trens.

Rota completa:

```
Molinari → 8 min a pé → Chinatown–Rose Pak → Linha T →
4th & King → Caltrain → Menlo Park → Shuttle M3 (grátis) → escritório
```

Cerca de **1h15** e **$11–17**. Não desça em Atherton: quase nenhum trem para lá e o shuttle não passa.

> A última corrida do M3 sai por volta das **17h35** e não há serviço no fim de semana. Esse é o horário-âncora para sair do escritório.

## Persistência

Os checkboxes das listas de compras e a última aba aberta ficam salvos em `localStorage`, com fallback em memória caso o navegador bloqueie o acesso. Nada sai do aparelho — não há backend.

O botão **Limpar lista semanal** zera a compra da semana para você recomeçar no domingo.

---

## Como publicar no GitHub Pages

```bash
# 1. Crie o repositório no GitHub (ex.: sf-um-mes)

# 2. Na pasta do projeto
git init
git add .
git commit -m "Guia de um mês em San Francisco"
git branch -M main
git remote add origin https://github.com/SEU-USUARIO/sf-um-mes.git
git push -u origin main
```

Depois, no GitHub: **Settings → Pages → Source: Deploy from a branch → Branch: `main` / `(root)` → Save**.

Em 1–2 minutos o app estará em `https://SEU-USUARIO.github.io/sf-um-mes/`.

## Como instalar no celular

**iPhone (Safari):** abra a URL → botão Compartilhar → *Adicionar à Tela de Início*.
**Android (Chrome):** abra a URL → menu ⋮ → *Instalar app*.

Depois de instalado, funciona offline — útil no túnel do Muni e nos trechos sem sinal do Caltrain.

> **Nota sobre offline:** as fontes vêm do Google Fonts e são cacheadas na primeira visita online. Se você quiser garantia total de offline desde o primeiro uso, baixe os `.woff2` para uma pasta `fonts/`, troque o `<link>` por `@font-face` local e adicione os arquivos ao array `ASSETS` no `sw.js`.

## Atualizando o conteúdo

Todo o conteúdo é HTML direto no `index.html` — edite o texto e dê push. As listas de compras estão no bloco `<script>`, nos arrays `setupList` e `weekList`, no formato `{n:'nome do item', q:'quantidade'}`.

Ao mudar arquivos, incremente a versão do cache no `sw.js` (`sf-guia-v3` → `sf-guia-v3`) para forçar a atualização nos aparelhos já instalados.

## Estrutura

```
.
├── index.html      # app inteiro: HTML, CSS e JS
├── manifest.json   # metadados do PWA
├── sw.js           # service worker (cache-first)
├── icons/
│   ├── icon-192.png
│   ├── icon-512.png
│   └── icon-maskable-512.png
└── README.md
```

---

**Horários, tarifas e regras mudam.** Confirme no app do Caltrain, do Muni e no site do ELI antes de sair.
