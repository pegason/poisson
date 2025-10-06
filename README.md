# Tabela do Brasileirão (local)

Projeto simples que carrega dados de `banco_jogos.csv` e exibe uma tabela de classificação.

Como usar

- Coloque o arquivo `banco_jogos.csv` na mesma pasta que o `index.html` (já existente no workspace).
- Abra `index.html` diretamente no navegador (duplo clique) ou rode um servidor estático local para evitar problemas de CORS.

Opções para rodar localmente (Windows / PowerShell):

- Abrir direto (pode falhar por CORS em alguns navegadores):

```powershell
# Simulador Poisson — Campeonato Brasileiro 2025

Este projeto é uma página web estática que usa a Distribuição de Poisson para modelar e simular os resultados das partidas do Campeonato Brasileiro (versão didática para TCC). Ele carrega jogos reais e fixtures restantes a partir de arquivos CSV (`banco_jogos.csv` e `banco_restante.csv`) e executa simulações (Monte Carlo) para estimar probabilidades de campeão, vagas na Libertadores, Sul‑Americana e rebaixamento.

## Origem e vínculo acadêmico
Este repositório e a aplicação foram desenvolvidos como parte da dissertação/TCC do autor (José Marques da Fonseca Junior). O trabalho apresenta a fundamentação teórica, fórmulas, experimentos e discussão dos resultados — o texto da dissertação contém detalhes sobre: hipótese de modelagem, métricas de ajuste (log‑verossimilhança, qui‑quadrado, bootstrap), e recomendações para uso didático e análises posteriores.

Características relevantes relacionadas à dissertação:
- Objetivo pedagógico: projeto pensado para apoiar um TCC/dissertação com explicações didáticas e exemplos reproduzíveis.
- Reprodutibilidade: todos os dados necessários (CSV) e o código são fornecidos no repositório para permitir replicação dos experimentos.
- Modelo estatístico: base no modelo Poisson independente por equipe, estimativa empírica de parâmetros e fator de vantagem de jogar em casa (home advantage).
- Validação sugerida: o texto da dissertação recomenda comparações por log‑likelihood, testes de calibração e bootstrap para intervalos de confiança das probabilidades obtidas por Monte Carlo.
- Limitações e extensões: o trabalho discute limitações do modelo (não captura dependência entre gols) e aponta caminhos para modelos bivariados ou GLMs mais sofisticados.

## Linguagens e tecnologias
- HTML, CSS e JavaScript (front-end puro, sem frameworks de build).
- Tailwind CSS (via CDN) para utilitários de estilo.
- KaTeX (via CDN) para renderização de fórmulas matemáticas.
- Código JavaScript implementa o parser CSV, normalização/fuzzy-match de nomes, cálculo de estatísticas e o modelo estatístico baseado em Poisson.

## Principais conceitos e funcionalidades
- Parser CSV tolerante a formatos e header flexível.
- Normalização de nomes e correspondência fuzzy (Levenshtein) para mapear times entre diferentes arquivos.
- Estimativa de "home advantage" a partir dos jogos já disputados.
- Modelo de gols: Poisson para cada time; probabilidades de resultado a partir do produto das PMFs (distribuição conjunta de placares).
- Simulação Monte Carlo de temporada (configurável), agregando probabilidades de: campeão, Top‑4 (Libertadores), Top‑6, Sul‑Americana (7–12) e rebaixamento (17–20).
- UI interativa: navegação rodada‑a‑rodada, visualização de partidas simuladas, mini‑barras de probabilidade por time, e listagem dos placares mais prováveis por partida.
- Acessibilidade: ARIA, live regions, foco visível, tooltips e labels nas barras de probabilidade.

## Como rodar localmente
> Observação: o navegador bloqueia `fetch()` em `file://`. Rode um servidor HTTP simples na pasta do projeto.

1. Abra um terminal na pasta do projeto (`c:\Users\rodri\projetos\pai`).
2. Execute (Python instalado):

```powershell
python -m http.server 5500
```

3. Abra no navegador: `http://localhost:5500`
4. A interface carregará os CSVs `banco_jogos.csv` (resultados) e `banco_restante.csv` (fixtures). Use os controles Monte Carlo para rodar simulações (ex.: "MC 500 (final)").

## Deploy (GitHub + Netlify)
- O projeto é um site estático e pode ser hospedado gratuitamente em Netlify conectado ao repositório no GitHub.
- Passos básicos:
	1. Faça commit e push do repositório para um repositório no GitHub.
	2. No Netlify, crie um novo site -> "Import from Git" -> selecione o repositório.
	3. Como este é um site estático sem build, defina: Build command: (vazio) e Publish directory: `/` (ou a pasta onde está o `index.html`).
	4. Conecte e publique. Netlify fará deploy automaticamente a cada push (se configurado).

Observação: se usar recursos externos (APIs, CSVs remotos), configure CORS adequadamente.

## Estrutura mínima dos arquivos de dados
- `banco_jogos.csv` — histórico de partidas (colunas: RODADA;Home;Away;HG;AG;Res). Resultado (Res) pode ser `H`, `A`, `D`.
- `banco_restante.csv` — fixtures restantes (mesmo formato; colunas de gols vazias para partidas futuras).

## Boas práticas e limitações
- O modelo Poisson independente é simples e ótimo para material didático, mas não captura dependências entre os gols das equipes. Para análises científicas mais rigorosas considere modelos bivariados ou GLMs com variáveis explicativas.
- Monte Carlo roda no main thread; para grandes números de simulações (>2000) recomendo mover a execução para um Web Worker para não travar a UI.

## Créditos
- Autor / Projeto: José Marques da Fonseca Junior — TCC 2025
- Repositório: (link para o GitHub do projeto)
- Deploy: Netlify (site automático a partir do GitHub)

## Contato
- Se quiser que eu adicione recursos (Web Worker, export CSV, botão fixar placar), diga qual item priorizar.

---
README gerado automaticamente pelo assistente de desenvolvimento — adapte os links do repositório/Netlify conforme necessário.
