# Estado

Atualizado em 2026-11-19.

## Base

O fork parte do `main` do upstream em `f190399` (v1.6.2 mais um commit de créditos no README).
Nenhuma mudança de código do fork ainda.

## Verificado no fork (2026-11-20, Windows 11, RTX 5080, MSYS2 CLANG64 com clang 22.1.8)

- `bash build.sh` compila `out/vwport.exe` sem erros.
- Testes: 164 testes Python passam (30 pulados no Windows) e os 8 testes nativos do CMake passam
  (png-decode, perf-overlay, graphics-settings, gpu-platform, services, pad-map, mp3, videodec).
- O jogo inicia a partir do código (`run.py`) com o renderer nativo numa GPU NVIDIA: 1726 shaders
  traduzidos (2 falham, os já conhecidos), 29 hooks instalados, frames desenhados por 55 s nas
  telas iniciais, sem erro no log. Ninguém jogou nem olhou a imagem nessa execução.

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
