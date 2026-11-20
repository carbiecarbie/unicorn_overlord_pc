# Unicorn Overlord PC (fork) - instruções para agentes

Fork de [hachi23/unicorn_overlord_pc](https://github.com/hachi23/unicorn_overlord_pc), que o
autor original deixou de desenvolver em 2026-11-18. É um port nativo (Linux e Windows) da versão
de PS4 de Unicorn Overlord: o executável do jogo roda direto na CPU do PC, e o projeto fornece o
sistema do PS4 (`src/runtime_*.c`) e o renderer Vulkan (`src/native_*.c`, `gpu/platform/`).
Licença: GPL-2.0-or-later.

- `origin`: o fork (carbiecarbie). `upstream`: o repositório original, só para leitura.
- Visão geral do código: `README.md`. Renderer: `docs/dev/NATIVE_RENDERER.md`.

## Regras

- **Nada do jogo entra no repositório**: dump, `eboot.bin`, arquivos `.CPK` (PS4 ou Switch),
  shaders convertidos, saves, capturas de tela do jogo ou dumps de frame. Ver `CONTRIBUTING.md`.
- O dump fica fora do repositório; aponte para ele com `VW_GAME_DIR`.
- Verifique mudanças gráficas por imagem (`tools/native/parity.sh`), não por "rodou".
- Não faça commit nem push sem autorização do mantenedor.

## Como compilar, rodar e testar

- Windows: shell MSYS2 CLANG64, `bash build.sh` (detalhes em `packaging/windows/README.md`).
- Linux: `bash build.sh`.
- Rodar da árvore de código: `VW_GAME_DIR=<dump> VW_DATA_DIR=run_uo python3 run.py`.
- Testes: `python -m unittest discover -s tests`, `bash build.sh --test` e os testes de GPU
  listados em `packaging/test-native.sh`.

## Memória do projeto

Fica em `docs/memoria/`. Leia antes de começar e atualize antes de encerrar uma sessão que mudou
arquivos ou tomou decisões.

- `docs/memoria/estado.md`: o que funciona hoje e o que está em andamento.
- `docs/memoria/decisoes.md`: decisões tomadas, com data e motivo.
- `docs/memoria/handoff.md`: o que a última sessão fez, pendências e próximos passos.

`docs/dev/HANDOFF.md`, `docs/dev/ROADMAP.md` e `docs/dev/unicorn/` são as notas do autor original:
referência técnica e histórico até a v1.6.2, não o estado atual do fork.
