# KOF Genkai — modelos

Modelos (bots) do KOF Genkai: o Iori (KOF2002) treinado por imitação e reforço contra a CPU.
Cada modelo é um par `<nome>.onnx` + `<nome>.json`, publicado nos assets das releases deste repositório;
o app (PC e Android) lista as releases e baixa o par escolhido.

| modelo | o que é |
|---|---|
| `iori_cpu_v010` | base CPU, modo single |
| `iori_cpu_v020` | base CPU, modo trios |
| `iori_cpu_v021` | base CPU, trios; zera o arcade em ~91% (temp 0,25) |
| `iori_hum_v010_joker` | base humana (estilo de jogadores reais), single; zera em ~84% |
| `iori_hum_team_c5` | base humana, trios (estilos 1, 2, 6, 8), ciclo de treino em andamento |

## Formato

- `.onnx` (opset 17): entradas `state` float32 [B,180,31] (features cruas), `chars` int64 [B,180,2]
  (id do personagem + 1), `acts` int64 [B,180,2], `player` int64 [B] (estilo); saída `logits` [B,A]
  da última posição. A normalização já está dentro do modelo.
- `.json`: vocabulário de ações, `pad_tab` (ação → controle absoluto, olhando para a esquerda/direita),
  janela, estilos disponíveis, temperatura e `hold` (decide a cada 2 frames).

Não há ROM, BIOS nem código do jogo aqui: só os pesos das redes.
