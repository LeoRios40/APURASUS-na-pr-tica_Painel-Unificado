# Guia de manutenção do Painel APURASUS

Este guia é para quem mantém o painel na DCFI. As unidades não precisam ler.

## Como o painel é feito

- O painel inteiro é **um arquivo só**: `index.html`. Textos, telas, ferramentas e bibliotecas (planilhas e PDF) estão dentro dele. Por isso funciona sem internet.
- O **link** (`https://leorios40.github.io/APURASUS-na-pr-tica_Painel-Unificado/`) mostra esse mesmo arquivo. Quem não tem internet usa uma cópia dele (botão **Baixar para usar sem internet**, no topo do painel aberto pelo link).
- O arquivo `versao.json` diz qual é a versão mais nova. Os painéis abertos com internet consultam esse arquivo e mostram o aviso "Existe uma versão mais nova".

## Publicar uma versão nova

**Pelo Claude (recomendado):** peça a mudança numa conversa e diga "atualize o painel APURASUS no GitHub". O Claude gera a versão, testa, envia o `index.html`, atualiza o `versao.json` e te manda o arquivo para distribuir offline.

**À mão, pelo site do GitHub:**
1. No arquivo novo, confira o número em `PAINEL_VERSAO` (veja abaixo).
2. No repositório, clique em **Add file › Upload files**, envie o arquivo com o nome **index.html** (substitui o antigo) e clique em **Commit changes**.
3. Abra o `versao.json`, clique no lápis, mude `"versao"`, `"data"` e `"resumo"` para os da versão nova e clique em **Commit changes**.
4. Em um ou dois minutos o link está atualizado. Quem estiver com o painel aberto recebe o aviso para atualizar.

> Sempre suba o `index.html` **antes** do `versao.json`. Se o aviso sair antes do arquivo novo, a pessoa clica em "Atualizar" e ainda vê a versão antiga.

## Onde mudar cada coisa dentro do `index.html`

Abra o arquivo num editor de texto (Bloco de Notas, Notepad++ ou VS Code) e procure com **Ctrl+F** pelo texto da coluna "Procure por". O arquivo é grande (cerca de 4 MB); prefira Notepad++ ou VS Code.

| O que mudar | Procure por | Observação |
|---|---|---|
| Número e data da versão | `const PAINEL_VERSAO` | Aumente o número a cada versão publicada. |
| Telefone e e-mails da DCFI do botão "Reportar um problema" | `const DCFI_CONTATO` | E-mails separados por vírgula. Mude também o texto do diálogo (procure por `A mensagem vai para`). |
| Regras do Analisador Produção (qual centro de custo vira qual item) | `ccLimpo.includes(` | A tabela da página Regras fica em `id="rg-producao"`: atualize as duas juntas. |
| Alíquotas (encargos) e provisão | `REGRAS_APURASUS` | Bloco `aliquotas`: uma linha por período (`de`, `ate`, `clt`, `est`, `mun`, `prov`). A conferência RH, o guia de encargos e a página Regras usam esse bloco. |
| Tabela de itens: fonte e onde lançar (conferências) | `REGRAS_APURASUS` › `fontes` | Usada pelas conferências. |
| Itens da página "Onde lanço?" (nome, centro de custo, fonte, observação, caminho) | `const D = [` | Uma lista por item, na ordem: nome, centro de custo, fonte, observação, classificação, caminho no APURASUS. |
| Item que mudou de nome no APURASUS | `const SINONIMOS` | Acrescente o nome novo ao lado do antigo para as conferências entenderem os dois (como foi feito com o Mais Médicos). |
| Vídeos do YouTube | `const OL_VIDEOS_LISTA` | Uma linha por vídeo: `id` (o código depois de `youtu.be/`), título, tema e onde ele aparece. |
| Palavras do dia a dia da busca | `const OL_SINON` | `p` = palavras que a unidade digita; `itens` = nome exato do item de custo; `guias` = passo a passo. |
| Página "Novidades" | `<div class="nv">` | Acrescente uma linha `nv-item` no topo da lista. |
| Textos dos tours | `const TOUR` | `GERAL` é o tour do painel (primeira visita e menu); `PAGINAS` tem um tour por página (o nome é o id da página, ex.: `conf-rh`). Cada balão tem o alvo (o que fica em destaque), o título `t` e o texto `x`. Para mostrar o tour de novo a todos, troque `apurasus_tour_v2` por `apurasus_tour_v3`. |
| Endereço do link oficial | `const PAINEL_LINK` | Só mude se o repositório for renomeado. |

## Depois de mudar à mão

1. Abra o arquivo no Chrome ou no Edge e confira a página que mudou.
2. Rode uma conferência com arquivos de teste para ver se nada quebrou.
3. Publique seguindo os passos acima.

Se algo der errado, o GitHub guarda todas as versões: em **Commits** dá para ver e recuperar qualquer `index.html` anterior.
