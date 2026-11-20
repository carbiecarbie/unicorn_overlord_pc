# Estado

Atualizado em 2026-11-19.

## Base

O fork parte do `main` do upstream em `f190399` (v1.6.2 mais um commit de créditos no README).
Nenhuma mudança de código do fork ainda.

## O que funciona (segundo o autor original, até a v1.6.2)

- Dump suportado: CUSA36381 (Ásia) v01.04, com ou sem o patch de inglês, e o pacote de Hong Kong
  1.05.
- Prólogo, capítulo 1 e sua primeira batalha jogados; salvar e carregar funcionam.
- Renderer nativo (experimental) a 60 FPS numa RX 560X; renderer shadPS4 disponível como
  alternativa (edição separada, branch `shadps4-edition`).
- Texto em inglês, francês, alemão, italiano e espanhol com os arquivos do Switch; mods de texto.

## O que não foi verificado ou falta

- Nada depois da primeira batalha do capítulo 1 foi jogado.
- A fase final travou no início com um save importado do Switch, nos dois renderers.
- Renderer: sem profundidade e culling, sem rect lists, 2 dos 3 compute shaders não rodam,
  2 shaders não encontrados (`e041714c`, `546af9ea`), caches sem limite.
- Windows com o renderer nativo, NVIDIA, Intel, Steam Deck e ultrawide não foram testados pelo
  autor.
- Issues e PRs abertos no upstream em 2026-11-19: #74, #91, #109, #110, #117 e os PRs #116,
  #118, #119 (não integrados).

## Em andamento

Nada.
