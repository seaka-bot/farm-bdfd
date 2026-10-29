# Farm

**Um jogo de fazenda dentro do Discord.** Você anda por um mapa 7×7 com botões, compra terreno, planta, espera crescer e colhe pra lucrar.

[Jogue a simulação no navegador](https://mnsa.com.br/projetos/farm/) · [Outros projetos do Seaka](https://github.com/seaka-bot)

> [!WARNING]
> **Código de acervo.** Foi escrito pra uma versão antiga do BDFD e não é mantido. Use como referência e adapte.

## Arquivos

| Arquivo | Gatilho no BDFD | O que faz |
|---|---|---|
| `prefix/farm.bdscript2` | o nome do comando (ex.: `farm`) | Abre a fazenda. Se faltar alguma variável, avisa qual criar e com que valor. |
| `oninteraction/farm.bdscript2` | `$onInteraction` | Todo o resto: andar, comprar terreno, a loja, plantar e colher. |

Os dois são **BDScript 2**.

## Variáveis

Crie no app do BDFD com estes valores padrão. Se esquecer alguma, o comando `farm` mostra o nome e o valor que falta.

| Variável | Padrão | Usada como | Pra que serve |
|---|---|---|---|
| `FarmMapa` | *(veja abaixo)* | usuário | O mapa de cada jogador: 49 números separados por `,` |
| `FarmFeira` | *(veja abaixo)* | global | A loja: as plantas à venda |
| `FarmStats` | `/////////////////////////////////////////////////` | usuário | O que está plantado em cada quadrado. Copie exatamente, com todas as barras. |
| `FarmCoins` | `500` | usuário | O dinheiro do jogador 🌱 |

**`FarmMapa`**
```
0,0,0,0,0,0,0,0,2,2,0,1,1,0,0,2,2,0,1,1,0,0,0,0,0,0,0,0,0,1,1,0,1,1,0,0,1,1,0,1,1,0,0,0,0,0,0,0,0
```

Cada número é um quadrado do mapa:

| Número | Quadrado |
|---|---|
| `0` | 🟩 grama |
| `1` | 🟪 terreno à venda (1000 🌱) |
| `2` | 🟫 terra, pronta pra plantar |
| `5` a `10` | 🌾 uma planta (o número é o ID dela na loja) |

**`FarmFeira`**
```
5:wheat:100:60:105/6:cotton:200:100:210/7:lavender:500:200:520/8:jasmin:1000:300:1050/9:potato:5000:1400:5300/10:bonsai:638:600000:10000
```

Cada planta é `id:nome:preço:tempo em segundos:revenda`, e as plantas são separadas por `/`.

| ID | Planta | Preço | Tempo | Revenda |
|---|---|---|---|---|
| 5 | wheat | 100 | 1 min | 105 |
| 6 | cotton | 200 | ~2 min | 210 |
| 7 | lavender | 500 | ~3 min | 520 |
| 8 | jasmin | 1000 | 5 min | 1050 |
| 9 | potato | 5000 | ~23 min | 5300 |
| 10 | bonsai | 638 | ~7 dias | 10000 |

## Emojis

Nenhum emoji customizado. Tudo é emoji padrão do Discord (🟩 🟪 🟫 🌾 🧑‍🌾 🌱), definido no começo do `oninteraction/farm.bdscript2`. Pra trocar, é só editar estas linhas:

```bdfd
$var[u;🧑‍🌾]
$var[0;🟩]
$var[1;🟪]
$var[2;🟫]
$var[5;🌾]
...
$var[FarmCoin;🌱]
```

## Permissões

O bot precisa de **Inserir links** (Embed Links) no canal.

## Como jogar

1. `farm` abre a fazenda. Aperte **Plant**.
2. Ande com ⬅️ ⬆️ ⬇️ ➡️. Você é o 🧑‍🌾.
3. Em cima de terra 🟫, aparece **Plant** → **Buy crops** → escolha com ⬆️ ⬇️ → **plant**.
4. Em cima de terreno 🟪, dá pra comprar por 1000 🌱.
5. Em cima de uma planta 🌾, aparece a barra de crescimento. Quando chegar a 100%, **harvest**.

> Andar pra fora do mapa é permitido **de propósito**.

## Limitações conhecidas

- O botão **Status** da tela inicial não tem resposta no código: clicar nele não faz nada.

## Técnicas usadas

- Laço gerado com `$eval`: [explicação geral](https://github.com/seaka-bot/.github/blob/main/TECNICAS.md#laço-com-eval)
- Mapa e loja numa string: [explicação geral](https://github.com/seaka-bot/.github/blob/main/TECNICAS.md#string-como-banco-de-dados)
- Estado no ID do botão (aqui separado por `#`): [explicação geral](https://github.com/seaka-bot/.github/blob/main/TECNICAS.md#estado-no-id-do-botão)

## Créditos

Por **hirozn** · [mnsa.com.br](https://mnsa.com.br)
