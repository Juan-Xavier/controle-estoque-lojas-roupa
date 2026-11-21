# Sistema de Controle de Estoque para Lojas de Roupas

> Projeto acadêmico — Engenharia de Software

## Links do projeto

- **Repositório:** https://github.com/Juan-Xavier/controle-estoque-lojas-roupa
- **Página do projeto (GitHub Pages):** https://juan-xavier.github.io/controle-estoque-lojas-roupa/
- **Página inicial:** [index.html](index.html)

> O repositório está criado e os arquivos estão sendo mantidos na branch `main`. Para disponibilizar a página, ative o GitHub Pages em **Settings → Pages → Deploy from a branch → main → /(root) → Save**. O endereço acima é o endereço esperado após a publicação.

## 1. Proposta inicial informal

A ideia é um software, disponibilizado na web e em aplicativo mobile, voltado para a orquestração e o controle diário da disponibilidade de roupas em lojas. O objetivo é dar visibilidade às quantidades e aos tamanhos disponíveis em tempo real.

No início do expediente, a lojista ou vendedora registra ou faz a leitura das peças disponíveis na loja, categorizando-as por modelo, cor, tamanho (PP, P, M, G, GG etc.), quantidade e localização inicial.

Durante o atendimento, a equipe consulta rapidamente quantas peças restam de determinado modelo e quais tamanhos estão disponíveis, sem precisar deixar a cliente esperando enquanto procura o produto. A consulta também informa a localização física da peça, que pode ser uma arara, vitrine, bolsa, prateleira ou depósito.

Sempre que uma peça é vendida, retirada ou transferida entre locais, a movimentação é registrada e o saldo é atualizado. O sistema sinaliza situações de estoque baixo — por exemplo, a última unidade M de uma blusa — para apoiar a reposição a partir do depósito.

Ao final do expediente, o sistema apoia o fechamento diário, comparando o estoque registrado com a contagem física e as movimentações do dia. A solução apresenta divergências e um Score de Acurácia para acompanhar a confiabilidade do inventário da loja. A fórmula desse score ainda precisa ser definida e validada com os responsáveis pela operação.

## 2. Análise da Pirâmide de Valor B2B

### Por que B2B é a análise principal?

O cliente direto do software é a empresa varejista — por meio do proprietário ou gestor da loja — que contrata ou decide adotar a solução. Vendedores, gerentes, estoquistas e financeiro são usuários ou áreas beneficiadas dentro da organização. Por isso, a proposta de valor principal é **B2B (Business to Business)**.

A Bain organiza os 40 elementos de valor B2B em cinco camadas: requisitos básicos (*table stakes*), valor funcional, facilidade de fazer negócios, valor individual e valor inspiracional. Foram selecionados apenas os elementos que podem ser relacionados às funcionalidades descritas; isso não significa que o produto já tenha sido implementado ou validado com clientes.

| Camada B2B | Elemento de valor | Como o projeto entrega esse valor |
|---|---|---|
| Requisitos básicos | Atender às especificações (*meeting specifications*) | Registrar e consultar estoque por modelo, cor, tamanho, quantidade e localização, com acesso web e mobile, conforme o propósito da solução. |
| Funcional — econômico | Redução de custos (*cost reduction*) | Diminuir o tempo gasto procurando peças e conferindo saldos, além de reduzir retrabalho associado a divergências. A economia efetiva deverá ser medida em uso real. |
| Funcional — econômico | Melhoria da receita (*improved top line*) | Ajudar a evitar vendas perdidas por demora ou falta de informação sobre tamanhos disponíveis. É um benefício potencial, não uma garantia de aumento de faturamento. |
| Facilidade de fazer negócios — produtividade | Economia de tempo (*time savings*) | A consulta rápida de quantidade, tamanho e localização reduz o tempo entre a solicitação da cliente e a resposta da vendedora. |
| Facilidade de fazer negócios — produtividade | Redução de esforço (*reduced effort*) e diminuição de transtornos (*decreased hassles*) | Reduzir buscas físicas e conferências manuais para descobrir onde está cada peça ou se existe determinado tamanho. |
| Facilidade de fazer negócios — produtividade | Informação e transparência (*information* e *transparency*) | Exibir quantidades, tamanhos, localizações, movimentações e divergências em um único ponto de consulta. |
| Facilidade de fazer negócios — operacional | Organização e simplificação (*organization* e *simplification*) | Organizar o estoque por produto, variação e localização física, estruturando consulta, movimentação e reposição. |
| Facilidade de fazer negócios — operacional | Integração (*integration*) | Fazer com que web e mobile trabalhem sobre os mesmos dados de estoque. Integração com caixa/ERP não está definida no escopo atual. |
| Facilidade de fazer negócios — estratégico | Redução de riscos (*risk reduction*) | Reduzir decisões baseadas em saldos incorretos e o risco de não localizar uma peça que aparece como disponível. |
| Valor individual — pessoal | Redução da ansiedade (*reduced anxiety*) | Dar mais confiança a vendedores e gestores ao consultar informações atualizadas, em vez de depender de estimativas. |

### Elementos B2B não selecionados

A proposta atual não sustenta afirmar valores inspiracionais como visão, esperança ou responsabilidade social; ganhos individuais ligados a carreira, reputação ou expansão de rede; nem elementos de relacionamento com o fornecedor do software, como especialização, compromisso e estabilidade. Esses valores dependeriam de serviços ou resultados ainda não descritos.

## 3. Análise da Pirâmide de Valor B2C

### Por que também analisar B2C?

A cliente da loja não é, pela proposta atual, compradora nem usuária direta do software. Ela recebe benefícios indiretos: a vendedora consegue responder mais rapidamente se existe o modelo e o tamanho procurados e localizar a peça com menos demora. Assim, a análise B2C descreve o **valor percebido pela consumidora final na experiência de compra**, enquanto a análise B2B descreve o valor para a loja que adota o sistema.

A pirâmide B2C da Bain reúne 30 elementos em quatro categorias: funcional, emocional, transformador (*life changing*) e impacto social. Para este projeto, os elementos mais aderentes estão nas camadas funcional e emocional.

| Camada B2C | Elemento de valor | Como a cliente percebe esse valor |
|---|---|---|
| Funcional | Economiza tempo (*saves time*) | Recebe uma resposta mais rápida sobre o modelo e o tamanho, sem esperar a vendedora procurar em vários pontos da loja. |
| Funcional | Reduz esforço (*reduces effort*) | Não precisa acompanhar a equipe em buscas pela loja nem repetir a solicitação em diferentes locais. |
| Funcional | Evita transtornos (*avoids hassles*) | A localização física registrada ajuda a equipe a encontrar a peça, reduzindo idas e vindas e interrupções no atendimento. |
| Funcional | Informa (*informs*) | Recebe uma informação mais confiável sobre quais tamanhos e quantidades estão disponíveis. |
| Emocional | Reduz ansiedade (*reduces anxiety*) | Uma resposta clara e rápida diminui a incerteza sobre conseguir experimentar ou comprar o tamanho desejado. |

### Elementos B2C não selecionados

O sistema melhora uma etapa da experiência de compra, mas não há base para afirmar que promove transformação de vida, autorrealização ou impacto social amplo. Outros elementos emocionais, como entretenimento, nostalgia, status ou atração, também não são entregues diretamente pelas funcionalidades descritas.

## 4. Conclusão: proposta de valor integrada

A proposta de valor central é **B2B**: ajudar lojas de roupas a manter um estoque mais organizado, visível e confiável, economizando tempo operacional, apoiando o atendimento e reduzindo riscos de divergência e perda de venda por falta de informação.

O valor **B2C** é complementar e indireto: a consumidora recebe atendimento mais ágil, com informação mais confiável e menos espera para localizar o tamanho desejado. Em resumo, **a loja compra a solução pela eficiência e pelo controle; a cliente sente o benefício na qualidade do atendimento**.

As relações apresentadas são hipóteses de valor derivadas da proposta funcional do projeto. Para validá-las, recomenda-se conversar com proprietários/gerentes, vendedores, estoquistas e clientes e observar o tempo de atendimento, a frequência de divergências e a ocorrência de vendas perdidas por indisponibilidade não identificada.

## 5. Referências

1. **Bain & Company.** *The Elements of Value* — modelo B2C: 30 elementos organizados em quatro categorias. Disponível em: https://media.bain.com/elements-of-value/. Acesso em: 21 nov. 2026.
2. **Bain & Company.** *The B2B Elements of Value* — modelo B2B: 40 elementos organizados em cinco categorias. Disponível em: https://media.bain.com/b2b-eov/index.html. Acesso em: 21 nov. 2026.
3. **Almquist, Eric; Cleghorn, Jamie; Sherer, Lori.** *The B2B Elements of Value*. Harvard Business Review, março de 2018. Disponível em: https://hbr.org/2018/03/the-b2b-elements-of-value.

---

## 6. Publicação no GitHub Pages

A página está publicada a partir do arquivo estático `index.html`, localizado na raiz do repositório. O GitHub Pages está configurado para publicar a branch `main` pela pasta `/(root)`.

Endereço do site: https://juan-xavier.github.io/controle-estoque-lojas-roupa/

Sempre que houver atualização na branch `main`, o GitHub Pages reconstruirá e publicará o site automaticamente.

> **Status:** publicação confirmada pelo workflow de Pages do GitHub, com as etapas de construção e implantação concluídas com sucesso.
