# Handoff

Atualizado em 2026-11-19.

## O que a última sessão fez

- Criou o fork no GitHub e clonou com os submódulos (`imgui`, `LibAtrac9`).
- Adicionou o remote `upstream` (repositório original).
- Criou `AGENTS.md`, `CLAUDE.md` e `docs/memoria/`, direto no `main` do fork.

## Ambiente local

- A instalação de jogo para testes fica ao lado do clone, em
  `..\Unicorn.Overlord-game\Unicorn.Overlord-P2P` (programa v1.6.2 empacotado). O dump está em
  `data\game` (CUSA36381 v01.04 com o patch de inglês) e o texto oficial do Switch 1.05 em
  `data\languages\Unicorn_US.CPK`.
- O build a partir do código no Windows ainda não foi feito nesta máquina (precisa de MSYS2
  CLANG64).

## Pendências

- O ruleset "Protect main" do upstream não vem com o fork; decidir se o fork terá um.

## Próximos passos sugeridos

1. Montar o ambiente MSYS2 e compilar o `main` no Windows; rodar os testes.
2. Jogar além do capítulo 1 com `VW_FRAME_STATS=1` e anotar as linhas `Native:` do log.
3. Avaliar os PRs abertos do upstream (#116, #118, #119) para integrar no fork.
