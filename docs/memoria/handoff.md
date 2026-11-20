# Handoff

Atualizado em 2026-11-20.

## O que a última sessão fez

- Criou o fork, clonou com os submódulos e adicionou o remote `upstream`.
- Criou `AGENTS.md`, `CLAUDE.md` e `docs/memoria/`, direto no `main` do fork.
- Instalou os pacotes CLANG64 no MSYS2 (`C:\msys64`), compilou o `main` e rodou os testes: tudo
  passou (detalhes em `estado.md`).
- Iniciou o jogo a partir do código por 55 s (RTX 5080): sem erros no log.
- Revisou e integrou no `main` os PRs #116, #118 e #119 do upstream e o branch de memória do
  renderer, com três ajustes do fork (ver `estado.md` e `decisoes.md`).

## Ambiente local

- Build: `bash build.sh` no shell MSYS2 CLANG64, ou de fora dele com `MSYSTEM=CLANG64` e
  `C:\msys64\usr\bin\bash.exe -lc`. Leva cerca de 12 s.
- Testes nativos no build de desenvolvimento: os alvos `*-test` do CMake em `out/gpu`
  (`packaging/test-native.sh` espera `out/gpu-static`, do build `--static`).
- Rodar: `VW_GAME_DIR=<dump> VW_DATA_DIR=run_uo py -3 run.py`. `run_uo/` está no `.gitignore`.
- A instalação de jogo para testes fica ao lado do clone, em
  `..\Unicorn.Overlord-game\Unicorn.Overlord-P2P` (programa v1.6.2 empacotado). O dump está em
  `data\game` (CUSA36381 v01.04 com o patch de inglês) e o texto oficial do Switch 1.05 em
  `data\languages\Unicorn_US.CPK`.
- `run_uo` não tem a pasta `languages`: rodando do código, o inglês vem do patch. Para usar o
  texto do Switch, copie o `Unicorn_US.CPK` para `run_uo\languages` ou defina `VW_LANGUAGES_DIR`.

## Pendências

- O ruleset "Protect main" do upstream não vem com o fork; decidir se o fork terá um.
- O build `--static` e o empacotamento (`packaging/windows/build.sh`) ainda não foram feitos.
- Na execução de teste as telas iniciais ficaram em cerca de 33 FPS com a janela sem foco; não
  foi investigado se é o jogo (telas de logo) ou limitação com a janela em segundo plano.

## Próximos passos sugeridos

1. Jogar além do capítulo 1 com `VW_FRAME_STATS=1` e anotar as linhas `Native:` do log; conferir
   na tela o Fit, o Stretch e o mouse no mapa de batalha.
2. Fazer uma sessão longa (mais de 90 minutos) para exercitar a correção de memória.
3. Fazer o build `--static` e o pacote para Windows.
