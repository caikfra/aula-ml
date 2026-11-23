# Versionamento de Dados e Modelos (`aula-ml`)

Repositório da Atividade Prática 07 da disciplina Engenharia de Sistemas Inteligentes (CK0444 – UFC), demonstrando o versionamento de datasets, partições e modelos com Git e DVC.

## Pré-requisitos

- **Git** (controle de versão de código, descritores `.dvc`, manifestos e relatórios)
- **Python 3.10+** (execução do treinamento e verificação de integridade usando apenas a biblioteca padrão)
- **DVC 3.x** (`pip install "dvc>=3,<4"` ou `pipx install 'dvc>=3,<4'`)

## Configuração do Armazenamento DVC

Os arquivos de dados (`data/chamados.csv`, `data/split.csv`) e o modelo (`models/model.json`) são armazenados fora do Git, em um remote DVC local configurado em `.dvc/config`:

- **Remote padrão:** `storage`
- **Caminho relativo:** `../dvc-storage` (pasta irmã ao diretório clonado)

Para verificar a configuração após clonar:

```bash
dvc remote list
```

Caso o armazenamento esteja em outro caminho local, atualize o remote com:

```bash
dvc remote modify storage url /caminho/para/dvc-storage
```

## Restauração de uma Versão Anterior

Para recuperar os artefatos exatos de uma versão publicada (por exemplo, `modelo-r1`) em um clone limpo, sem executar novo treinamento:

```bash
git clone <URL-DO-REPOSITORIO> aula-ml-restauracao
cd aula-ml-restauracao
git switch --detach modelo-r1
dvc pull
```

Para restaurar a segunda versão, substitua a tag por `modelo-r2`.
