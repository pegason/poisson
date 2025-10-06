# Relatório: Modelo Poisson para Previsão de Jogos de Futebol

Projeto: **A Distribuição de Poisson Aplicada à modelagem de resultados de jogos de futebol: Uma proposta didática para o Ensino Médio**

Feito por: José Marques da Fonseca Junior — Ano: 2025

## Objetivo

Apresentar, implementar e validar um modelo didático baseado na distribuição de Poisson para prever resultados de partidas de futebol e estimar a classificação final do Campeonato Brasileiro 2025 por simulação de Monte Carlo.

## Modelo e pressupostos

- Supomos que o número de gols marcados por cada equipe em uma partida segue uma distribuição de Poisson independente com parâmetro $\lambda$.

- A PMF de Poisson é dada por:

$$
P(K=k;\lambda)=\frac{e^{-\lambda}\lambda^{k}}{k!}
$$

- Estimativa de $\lambda$ utilizada (forma didática):

\(\lambda_{home} = \text{avgGF}_{home} \times \frac{\text{avgGA}_{away}}{\text{leagueAvgGA}} \times \text{homeAdv}\)

\(\lambda_{away} = \text{avgGF}_{away} \times \frac{\text{avgGA}_{home}}{\text{leagueAvgGA}}\)

onde:
- avgGF_time = média de gols marcados por jogo pelo time (no que já foi jogado);
- avgGA_opponent = média de gols sofridos pelo adversário;
- leagueAvgGA = média de gols sofridos por jogo na liga (global);
- homeAdv = fator de vantagem de jogar em casa, estimado a partir dos dados.

## Estimativa da vantagem de jogar em casa (homeAdv)

No código a vantagem de jogar em casa é estimada como a razão entre média de gols marcados em casa e média de gols sofridos fora, calculada sobre os jogos já disputados:

\(\text{homeAdv} \approx \dfrac{\text{mean gols mandante}}{\text{mean gols visitante}}\)

Para estabilidade, o valor é limitado entre 0.7 e 1.3. O valor estimado é mostrado na interface (campo de status) quando a página carrega.

## Cálculo de probabilidades de resultado

Assumindo independência entre os gols das equipes, a probabilidade de cada placar $(i,j)$ é:

$$
P(G_m = i, G_v = j) = P_{Poisson}(i;\lambda_m) \times P_{Poisson}(j;\lambda_v)
$$

A probabilidade de vitória do mandante é a soma sobre todos os pares com $i>j$, empate soma dos pares $i=j$, e vitória visitante $i<j$.

No código essa soma é aproximada truncando as PMFs até um Kmax adaptativo.

## Validação e métricas sugeridas

- Log-verossimilhança para comparar modelos (Poisson vs. NegBin).
- Qui-quadrado de Pearson / Deviance para contar discrepâncias entre observados e esperados por número de gols.
- Bootstrap e Monte Carlo para obter intervalos de confiança nas probabilidades de classificação.
- Calibration plot e Brier score para avaliar calibração das probabilidades de resultados (H/D/A).

## Uso e reprodução

1. Coloque `banco_jogos.csv` (jogos já disputados) e `banco_restante.csv` (partidas futuras) na mesma pasta do `index.html`.
2. Sirva os arquivos via HTTP local (ex.: `python -m http.server 5500`) e abra `http://localhost:5500/index.html`.
3. A interface mostrará o valor estimado de `homeAdv` no status e usará essa estimativa nas simulações.

## Observações finais

- O modelo é propositalmente simples e ideal para fins didáticos. Para aplicações de previsão mais precisas, recomenda-se adotar modelos bivariados, GLMs com efeitos de time/temporada, ou modelos que incorporem covariáveis (lesões, deslocamento, calendário apertado).

- Para executar simulações grandes sem bloquear a interface, recomenda-se mover o Monte Carlo para um Web Worker (próxima etapa sugerida).

---

Arquivo gerado automaticamente. Verifique o valor de `homeAdv` no painel de status da página web após carregar os CSVs.
