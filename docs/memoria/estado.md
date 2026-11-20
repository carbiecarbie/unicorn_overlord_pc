# Estado

Atualizado em 2026-11-20.

## Base

O fork parte do `main` do upstream em `f190399` (v1.6.2 mais um commit de créditos no README).

Integrado no fork em 2026-11-20 (merge `7166790`):

- PR #116 do upstream: caminhos do `launcher.json` relativos à pasta do programa.
- PR #118: opção **Screen fit** (Fit ou Stretch) para telas que não são 16:9.
- PR #119: os dois acima com as correções do autor (migração do launcher, mouse, repaint).
- Branch `fix/native-renderer-memory`: libera render targets redimensionados, descarta
  texturas ociosas quando falta memória de vídeo e transborda vértices acima de 64 MiB.
- Ajustes do fork: mouse do mapa de batalha em 21:9 no caminho de estimativa, `screen_fit` no
  diagnóstico, `NATIVE_RENDERER.md` atualizado. O handoff de Linux do autor ficou de fora.

## Verificado no fork (2026-11-20, Windows 11, RTX 5080, MSYS2 CLANG64 com clang 22.1.8)

- `bash build.sh` compila `out/vwport.exe` sem erros.
- Testes: 179 testes Python passam (30 pulados no Windows) e os 9 testes nativos do CMake passam
  (png-decode, perf-overlay, graphics-settings, gpu-platform, services, pad-map, mp3, videodec,
  native-memory).
- O jogo inicia a partir do código (`run.py`) com o renderer nativo numa GPU NVIDIA: 1726 shaders
  traduzidos (2 falham, os já conhecidos), 29 hooks instalados, frames desenhados por 55 s nas
  telas iniciais, sem erro no log. Repetido depois da integração em Fit, em Stretch e em 21:9.
  Ninguém jogou nem olhou a imagem nessas execuções.

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
  2 shaders não encontrados (`e041714c`, `546af9ea`), cache de pipelines sem limite.
- A correção de memória do renderer só foi testada com falta de memória simulada, não na
  GTX 1080 que relatou as falhas (após 44 a 91 minutos). O transbordo de vértices não tem teto.
- O que foi integrado nunca rodou no Linux (o CI de Linux do upstream falhou antes de compilar,
  por erro 503 do servidor de pacotes).
- Um `VW_DATA_DIR` relativo em build empacotado passa a ser lido a partir da pasta do programa;
  quem usava isso antes pode começar com a pasta de dados vazia (os saves não são apagados).
- Windows com o renderer nativo, NVIDIA, Intel, Steam Deck e ultrawide não foram testados pelo
  autor.
- Issues abertas no upstream em 2026-11-19: #74, #91, #109, #110, #117.

## Em andamento

Nada.
