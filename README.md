# Fut de Terça — organizador de times

App de página única (`index.html`, sem build, sem backend, sem banco de dados) pra organizar os times do futsal de terça: cadastro por ordem de chegada, cronômetro de partida, gol + assistência, e estatísticas no fim da noite.

## Jogadores por time

Antes de cadastrar o primeiro jogador, a tela de Fila mostra um seletor de **jogadores por time** (atalhos pra Futsal = 4, Fut7 = 7, Campo = 11, ou qualquer número customizado). Assim dá pra usar o mesmo app numa pelada de campo ou num fut7, não só no futsal de terça.

Esse número **trava assim que o primeiro jogador é adicionado** — pra mudar, é só encerrar a sessão (🗑) e configurar de novo antes do próximo jogador entrar. Isso evita bagunçar times que já foram montados com outro tamanho.

## Como funciona a fila de times

- Os **2× o tamanho do time** primeiros a chegar formam os dois primeiros times — pra já sair um confronto equilibrado. Ex.: no futsal (4 por time) são os 8 primeiros; no fut7, os 14 primeiros.
- Do jogador seguinte em diante, os times seguem só a ordem de chegada mesmo, sem numeração — são só "Time", um atrás do outro na fila.
- **Os dois times que entram em quadra são sempre chamados de Time Preto e Time Verde**, pra bater com as cores reais dos coletes de vocês. A cor **gruda em quem tá jogando, não num "papel" fixo**: se o Time Verde vencer, ele continua Verde na partida seguinte — ninguém troca de colete só porque virou "o time da vez". Quem entra desafiando de novo é que veste a cor que sobrou (a do time que acabou de sair).
- Depois da primeira partida, o time vencedor **fica** (vira "Time da vez", com a cor que já estava usando) e o time perdedor volta pro **fim da fila**, jogador por jogador, completando o time que estiver incompleto antes de abrir um time novo.
- Quem chega depois (ex.: Nicolas) sempre entra no fim da fila atual.

## Durante a partida

Enquanto uma partida está rolando, a aba Fila mostra os dois times que estão em quadra (Time Preto e Time Verde, com uma tag "Em quadra") e, logo abaixo, o **próximo desafiante** — o time que vai encarar quem vencer. Como o confronto seguinte depende do resultado, não dá pra saber os dois lados antes da hora; por isso só o desafiante aparece, não uma "próxima partida" fechada.

## Fim de partida

O resultado **não precisa mais ser escolhido** — o app decide sozinho pelo placar (quem fez mais gols venceu). Isso muda dependendo de como a partida termina:

- **Tempo esgota sozinho**: sem popup nenhum. Se o placar tiver um vencedor, ele já vira "Time da vez" na hora. O celular vibra + toca um beep pra avisar (veja abaixo).
- **Você aperta "Encerrar partida agora"** (antes do tempo acabar): aparece um popup de confirmação — "Tem certeza que quer encerrar a partida agora?" — com o placar atual mostrado. Só depois de confirmar é que o resultado é processado. Cancelar não muda nada, a partida continua normalmente.
- **Empate** (placar igual, nos dois casos acima): como não dá pra saber sozinho quem fica, aparece a pergunta **"Empatou! Quem vai subir?"** com Time Preto, Time Verde, ou nenhum dos dois (os dois voltam pro fim da fila). Isso não conta como vitória nas estatísticas (só quem vence de verdade ganha ponto de "V"), mas o time escolhido continua como "Time da vez" — igual teria ficado se tivesse vencido.

## Editar a fila — toque no nome (sandbox)

Qualquer nome que aparece no app — na fila, no time da vez, em quadra jogando, ou nos goleiros fixos — é **tocável**. Ao tocar, abre um menu com as opções:

- **🔀 Trocar de lugar**: mostra todo mundo que dá pra trocar (fila inteira + time da vez + quem tá em quadra) e troca as posições dos dois, não importa em que time ou posição cada um esteja. É o jeito mais direto de reorganizar tudo do seu jeito — por exemplo, se alguém precisa sair no meio da partida, você pode trocar essa pessoa com quem quiser da fila pra ela entrar em quadra, sem precisar de nenhuma lógica especial: só troca e depois remove quem saiu.
- **🧤 Virar goleiro fixo**: pra quando alguém para de jogar na linha e passa a ficar só no gol. Tira a pessoa da fila de times (do mesmo jeito que o "Remover" abaixo — cascata ou substituição automática, conforme o caso) e a transforma em goleiro fixo: ela some da rotação de times, mas continua aparecendo nas opções de gol/assistência e nas estatísticas, exatamente como os goleiros cadastrados direto na seção deles. Só aparece pra quem ainda não é goleiro fixo.
- **✏️ Renomear**: abre um campo de texto já preenchido com o nome atual, pra corrigir erro de digitação.
- **✕ Remover**: tira a pessoa de onde ela estiver. O app decide sozinho o que fazer dependendo de onde ela está:
  - Se for **goleiro fixo**, só sai da lista de goleiros.
  - Se estiver **jogando a partida atual**, aciona a substituição automática (veja a seção abaixo — sobe o primeiro da fila no lugar dela, e pergunta se o substituto fica ou mantém a posição).
  - Se estiver **na fila normal ou no time da vez** (sem partida rolando), só sai — e a fila se recompacta sozinha (veja "efeito cascata" abaixo).

Em todos os casos — remover ou virar goleiro fixo — quem saiu da fila **continua nas estatísticas** com tudo que já tinha feito (gols, assistências, jogos).

## Remover jogador em quadra (ex.: machucou) e substituição

Ao remover (pelo menu acima) alguém que está **jogando a partida atual**:

1. O **primeiro jogador do próximo time da fila** sobe automaticamente pra completar a vaga (se não tiver ninguém na fila, o time simplesmente segue jogando com um a menos, sem travar nada).
2. Aparece um popup perguntando sobre esse substituto: **"Fica nesse time"** ou **"Mantém a posição na fila"**:
   - **Fica nesse time**: ele vira jogador normal desse time dali pra frente — se o time vencer (ou ficar no empate), ele continua como campeão junto com o resto; se perder, ele vai pro fim da fila junto com os outros, normalmente.
   - **Mantém a posição na fila**: ele só está ajudando por essa partida. No fim dela — **ganhe, perca ou empate o time** — ele não segue o destino do time: volta pra **frente da fila**, na posição em que estava antes de ser puxado como substituto (geralmente reformando o mesmo time de onde saiu).

Se preferir controlar isso manualmente em vez de deixar o app puxar sozinho, dá pra usar o **🔀 Trocar de lugar** pra colocar quem você quiser em quadra antes de remover a pessoa que vai sair — funciona igual, sem passar pelo popup de substituição.

### A fila sempre "sobe" pra cobrir vagas (efeito cascata)

Sempre que um time fica incompleto — seja porque alguém saiu da fila de espera, do time da vez, ou porque um substituto escolheu "manter a posição na fila" depois da partida — o app **puxa da frente da fila automaticamente** pra completar a vaga. E se puxar o primeiro de um time deixar ELE incompleto, o primeiro do próximo time sobe pra cobrir essa vaga, e assim por diante — em cascata, até o fim da fila (só o último time pode ficar incompleto, esperando gente nova chegar). Isso vale tanto na hora da substituição em quadra quanto depois que a partida termina.

## Goleiro fixo

Na aba Fila tem uma seção separada **"Goleiros fixos"**, com cadastro próprio. Quem entra ali:
- **Não entra na fila de times** (não ocupa vaga em nenhum Time Preto/Verde/genérico).
- Aparece com 🧤 do lado do nome, tanto na lista de goleiros quanto na tabela de Estatísticas.
- Pode ser selecionado normalmente pra marcar gol ou assistência, mesmo sem estar em nenhum dos dois times da partida.
- Editável pelo mesmo menu de tocar no nome (renomear/remover — trocar de lugar não se aplica, já que ele não faz parte da fila de times).

Dá pra cadastrar um goleiro fixo direto nessa seção, **ou converter alguém que já está jogando** a qualquer momento — mesmo no meio de uma partida — usando o **🧤 Virar goleiro fixo** no menu de tocar no nome (veja a seção acima).

## Gol de qualquer pessoa (inclui gol contra)

No modal de gol, depois dos botões rápidos com os jogadores do time escolhido, tem um **select "Foi outra pessoa? (gol contra, goleiro fixo...)"** com todo mundo cadastrado na sessão (fila + goleiros fixos). Isso cobre:
- **Gol contra**: você escolhe o time que marca o ponto e seleciona, no select, um jogador do time adversário como autor. O app detecta sozinho que é gol contra — soma o ponto pro time certo, mas **não conta como gol pessoal** do jogador nas estatísticas (aparece só como "(contra)" no log da partida e no histórico).
- **Goleiro fixo ou qualquer outro cadastrado** fazendo gol ou dando assistência, mesmo estando fora dos dois times daquela partida.

O mesmo select aparece no passo de assistência, pelo mesmo motivo.

## Aviso de fim de partida (vibração + som)

Quando o cronômetro chega a zero **sozinho** (não quando você aperta "Encerrar partida agora"), o celular vibra num padrão de chamar atenção e toca um beep curto. O áudio é destravado no toque de "Iniciar partida" (gesto do usuário), então funciona mesmo com a tela apagada ou em segundo plano na maioria dos Android.

> **Limitação:** vibração não funciona no iPhone/Safari — é bloqueio da própria Apple na Web, não tem contorno via navegador. Nesse caso só o beep sonoro dispara.

## Persistência (sem banco de dados)

Tudo fica salvo só no **localStorage do navegador** — ou seja, na sessão daquele aparelho. Não tem servidor, não tem banco, ninguém mais acessa esses dados. Dá pra fechar o navegador e reabrir que os times e o placar continuam do jeito que estavam.

No fim do fut, é só tirar o print da aba **Estatísticas** e apertar o 🗑 no topo (**Encerrar sessão**) pra limpar tudo e deixar pronto pra terça que vem.

> Importante: como é local ao navegador, se você jogar do celular, use sempre o mesmo navegador/aparelho durante aquela sessão (não vai sincronizar entre dois celulares ao mesmo tempo).

## Testar local

Só abrir o `index.html` direto no navegador (duplo clique) — funciona sem servidor nenhum.

## Deploy no Vercel

Duas formas, escolha a que preferir:

**Opção A — pelo site do Vercel (mais simples):**
1. Suba esse arquivo `index.html` pra um repositório no GitHub (pode ser um repo novo só com esse arquivo).
2. Entre em [vercel.com](https://vercel.com), "Add New… → Project", importe o repositório.
3. Vercel detecta que é estático (sem framework) — não precisa configurar build command nem output directory. Deploy.

**Opção B — pela linha de comando (mais rápido, sem GitHub):**
```bash
npm i -g vercel
cd pasta-onde-esta-o-index-html
vercel --prod
```
Ele pergunta umas coisas (nome do projeto, etc.) e te devolve a URL pública.

## Pequenas escolhas que fiz (me avisa se quiser diferente)

- **Duração da partida**: ajustável em botões de − / + (padrão 10 min, de 3 a 60).
- Tocar em qualquer nome abre o menu de editar (trocar de lugar / renomear / remover) — não tem mais o ✕ separado.
- Tem um **desfazer último gol**, pra quando clicar errado.
