# Comparação de Modelos (`chamados-r1` vs `chamados-r2`)

## Alteração Realizada

- **Dataset:** `chamados-v1` -> `chamados-v2` (tag `dados-v2`)
- **Mudança:** Correção do rótulo do chamado `006` (`bloqueio de acesso`) no conjunto de treino, de `comum` para `urgente`, alinhando-o à regra de rotulagem.
- **Partição:** `data/split.csv` mantida fixa (`split_sha256`: `2ef820171c1a4625fe216e6da67c7c8dcf9d97a08288c0239cd23f1a6961d981`).

## Tabela de Métricas

| Métrica | `chamados-r1` (`dados-v1`) | `chamados-r2` (`dados-v2`) | Variação |
| --- | :---: | :---: | :---: |
| Acurácia geral (n = 4) | 0.75 (3/4) | 1.00 (4/4) | +0.25 |
| Recall `urgente` (suporte = 2) | 0.50 (1/2) | 1.00 (2/2) | +0.50 |
| Recall `comum` (suporte = 2) | 1.00 (2/2) | 1.00 (2/2) | 0.00 |

## Hashes Verificados no Clone Limpo (`modelo-r1`)

Restauração validada em clone limpo (`aula-ml-restauracao`) via `git switch --detach modelo-r1` e `dvc pull`:

- **Commit SHA (`modelo-r1`):** `af8ab6af709a4d25f69b5f62d0d0f391862457bc`
- `data/chamados.csv`: `bc3fd86a3a5f598841a58839a9726d901fa7e8361ffe79c5b43873ad8a1328ac` (OK)
- `data/split.csv`: `2ef820171c1a4625fe216e6da67c7c8dcf9d97a08288c0239cd23f1a6961d981` (OK)
- `models/model.json`: `72a3a67936139a3473838a6dcfa7aae1acb4c23467be1ef1056d51d485b94840` (OK)

## Decisão

**Aceitar `chamados-r2`.**

- **Critério:** Melhorar o recall da classe `urgente` sem reduzir o recall da classe `comum`, avaliando na mesma partição de teste.
- **Justificativa:** Com a correção do rótulo de treino em `chamados-v2` e mantendo `data/split.csv` inalterado, o recall de `urgente` subiu de `0.50` para `1.00` e o recall de `comum` permaneceu em `1.00`, elevando a acurácia global de `0.75` para `1.00`.
