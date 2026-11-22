# Cenários dos Casos de Uso — Sistema de Controle de Estoque para Lojas de Roupas

Este documento apresenta os cenários principais e alternativos dos 15 casos de uso. Cada alternativa informa **a condição que a ativa** e **o que o sistema faz**.

## 1. Atores e objetivos

| Ator | Objetivo no sistema |
|---|---|
| Proprietário(a) | Acompanhar a confiabilidade do inventário por relatórios, indicadores e Score de Acurácia. |
| Gerente | Coordenar o estoque, manter produtos e locais cadastrados, acompanhar movimentações e alertas, fechar o dia e consultar resultados. |
| Vendedor(a) / Atendente | Verificar rapidamente modelo, cor e tamanho disponíveis, localizar peças e registrar vendas/saídas. |
| Estoquista / Repositor(a) | Registrar estoque inicial, entradas, reposições, transferências, locais e contagens físicas. |
| Financeiro | Consultar relatórios e histórico para apoiar conferências de movimentações e divergências. |

### Stakeholders que não são atores diretos nesta versão

A cliente é beneficiária indireta do atendimento mais rápido, mas não utiliza o software na proposta atual. O fornecedor também é beneficiário indireto, pois não há portal ou integração direta prevista. O responsável pela TI apoia a solução, mas ainda não possui uma funcionalidade administrativa definida. Esses papéis poderão se tornar atores caso o escopo seja ampliado.

## 2. Regras e premissas gerais

1. Web e mobile são canais de acesso aos mesmos dados; não são atores diferentes.
2. Cada quantidade está associada a um produto/variação (modelo, cor e tamanho) e a um local físico.
3. Uma movimentação só altera o saldo depois de validada e confirmada.
4. O sistema não permite saldo negativo.
5. O histórico deve registrar operação, item/variação, quantidade, origem/destino quando aplicável, data/hora e usuário responsável.
6. A última unidade é condição crítica prevista. Outros limites de estoque baixo precisam ser definidos pela loja.
7. A fórmula matemática do Score de Acurácia ainda precisa ser aprovada. O sistema não deve inventar um valor.

## 3. Cenários principais e alternativos

## UC01 — Cadastrar produtos e variações
**Ator:** Gerente. **Objetivo:** disponibilizar produtos e variações para controle do estoque.

**Principal:** 1. O gerente abre o cadastro. 2. O sistema apresenta o formulário. 3. O gerente informa nome/modelo e cadastra as combinações de cor e tamanho. 4. Confirma. 5. O sistema valida e grava produto e variações. 6. O sistema confirma o cadastro.

**Alternativas:**
- **A1 — Campo obrigatório ausente.** Condição: o gerente confirma com dados obrigatórios vazios. Resultado: o sistema indica os campos pendentes e mantém o formulário aberto; não grava.
- **A2 — Produto/variação possivelmente duplicado.** Condição: já existe registro equivalente, conforme a chave de identificação definida. Resultado: alerta sobre duplicidade e permite consultar ou corrigir o cadastro; não duplica automaticamente.
- **A3 — Cancelamento.** Condição: o gerente cancela antes de salvar. Resultado: descarta os dados não confirmados.

## UC02 — Configurar locais físicos da loja
**Atores:** Gerente; Estoquista/Repositor(a). **Objetivo:** cadastrar onde as peças podem ficar armazenadas ou expostas.

**Principal:** 1. O usuário acessa os locais. 2. O sistema lista os locais cadastrados. 3. O usuário adiciona identificação e categoria (arara, vitrine, prateleira, bolsa ou depósito). 4. Confirma. 5. O sistema valida, grava e confirma o novo local.

**Alternativas:**
- **A1 — Identificação incompleta.** Condição: nome ou categoria necessários não foram informados. Resultado: solicita correção e não salva.
- **A2 — Local duplicado.** Condição: já existe local com a mesma identificação. Resultado: alerta e oferece consulta ao local existente.
- **A3 — Cancelamento.** Condição: usuário cancela antes de confirmar. Resultado: não cria o local.

## UC03 — Registrar estoque inicial (abertura do expediente)
**Atores:** Estoquista/Repositor(a); Gerente. **Objetivo:** registrar as quantidades iniciais por produto, variação e local.

**Principal:** 1. O usuário abre o registro inicial. 2. Seleciona produto, cor e tamanho. 3. Informa quantidade física e local. 4. Repete para as variações e locais necessários. 5. Revisa e confirma. 6. O sistema valida e grava os saldos iniciais. 7. Confirma a abertura.

**Alternativas:**
- **A1 — Produto/variação não cadastrado.** Condição: item não existe no catálogo. Resultado: informa a ausência e orienta solicitar o cadastro; não registra quantidade para item inexistente.
- **A2 — Quantidade inválida.** Condição: quantidade vazia, negativa ou não numérica. Resultado: solicita correção e não grava a linha.
- **A3 — Local ausente.** Condição: a quantidade não foi associada a local. Resultado: solicita selecionar local cadastrado.
- **A4 — Abertura cancelada.** Condição: usuário cancela antes da confirmação final. Resultado: não conclui a abertura; dados não confirmados não alteram o saldo oficial.

## UC04 — Consultar disponibilidade por modelo, cor e tamanho
**Atores:** Vendedor(a)/Atendente; Gerente; Estoquista/Repositor(a). **Objetivo:** consultar quantas unidades existem por variação.

**Principal:** 1. O usuário abre a consulta. 2. Pesquisa pelo nome/modelo. 3. Aplica filtros de cor e tamanho, se desejar. 4. O sistema mostra as variações encontradas e quantidades disponíveis. 5. O usuário seleciona uma variação para ver mais detalhes.

**Alternativas:**
- **A1 — Produto não encontrado.** Condição: a pesquisa não corresponde a cadastro. Resultado: informa ausência de resultados e permite nova pesquisa.
- **A2 — Variação sem saldo.** Condição: o item existe, mas quantidade disponível é zero. Resultado: exibe indisponibilidade, sem sugerir que há unidades.
- **A3 — Filtro sem correspondência.** Condição: filtro não corresponde a valor cadastrado. Resultado: informa que não há resultados e permite limpar ou corrigir.

## UC05 — Consultar localização física da peça
**Atores:** Vendedor(a)/Atendente; Estoquista/Repositor(a). **Objetivo:** localizar fisicamente a peça solicitada.

**Principal:** 1. O usuário pesquisa o produto. 2. Seleciona cor e tamanho. 3. O sistema consulta os locais associados. 4. Exibe cada local e sua quantidade registrada. 5. O usuário usa a indicação para encontrar a peça.

**Alternativas:**
- **A1 — Saldo sem local associado.** Condição: existe quantidade, mas não há localização registrada. Resultado: informa que a localização está pendente e orienta registrar a transferência/movimentação correspondente.
- **A2 — Sem unidades disponíveis.** Condição: saldo da variação é zero. Resultado: informa indisponibilidade; não apresenta local como se houvesse peça.
- **A3 — Item não encontrado.** Condição: não existe produto/variação correspondente. Resultado: informa ausência e permite nova pesquisa.

## UC06 — Registrar venda ou saída de peça
**Ator principal:** Vendedor(a)/Atendente. **Ator autorizado adicional:** Gerente. **Objetivo:** registrar a retirada e atualizar o saldo. **Gatilho:** venda ou outra saída autorizada.

**Pré-condições:** usuário autorizado; produto e variação cadastrados; saldo e local de origem registrados.

**Pós-condições de sucesso:** movimentação gravada; saldo do local e da variação reduzido; condição de estoque crítico verificada. **Em falha:** nenhum saldo é alterado.

**Principal:**
1. O vendedor abre Registrar venda/saída.
2. O sistema solicita o produto.
3. O vendedor pesquisa e seleciona o modelo.
4. O sistema mostra cores, tamanhos, quantidades e locais.
5. O vendedor escolhe cor, tamanho e local de origem.
6. Informa a quantidade.
7. O sistema valida valor positivo e saldo suficiente.
8. O sistema apresenta o resumo da operação.
9. O vendedor confere e confirma.
10. O sistema registra tipo, item/variação, quantidade, origem, data/hora e usuário.
11. O sistema reduz os saldos correspondentes.
12. O sistema verifica se restou uma unidade ou se o limite de estoque baixo foi atingido.
13. O sistema confirma a saída e mostra o saldo atualizado e, se aplicável, o alerta.

**Alternativas:**
- **A1 — Produto/variação não encontrado.** Condição: pesquisa sem correspondência. Resultado: informa ausência, permite nova pesquisa e não registra saída.
- **A2 — Quantidade inválida.** Condição: campo vazio, zero, negativo ou não numérico. Resultado: solicita correção e retorna ao passo 6.
- **A3 — Saldo insuficiente.** Condição: quantidade solicitada supera o saldo do local. Resultado: informa o saldo disponível e impede confirmar; usuário pode ajustar quantidade ou localizar outra unidade.
- **A4 — Local de origem ausente.** Condição: vendedor não seleciona onde a peça está. Resultado: exige escolher local válido antes de prosseguir.
- **A5 — Cancelamento.** Condição: usuário cancela antes de confirmar. Resultado: descarta dados ainda não confirmados e mantém saldo.
- **A6 — Falha ao salvar.** Condição: erro de comunicação ou gravação. Resultado: informa que a operação não foi concluída e mantém saldo inalterado para evitar baixa parcial.

## UC07 — Registrar entrada ou reposição de peça
**Ator:** Estoquista/Repositor(a). **Objetivo:** adicionar unidades recebidas ou repostas ao estoque.

**Principal:** 1. Estoquista abre a função de entrada. 2. Seleciona produto, cor e tamanho. 3. Informa quantidade recebida e local de destino. 4. O sistema valida dados. 5. Apresenta resumo. 6. Estoquista confirma. 7. Sistema registra a entrada, aumenta o saldo e confirma.

**Alternativas:**
- **A1 — Item não cadastrado.** Condição: produto/variação não existe. Resultado: não registra; solicita cadastro/correção.
- **A2 — Quantidade inválida.** Condição: quantidade não positiva ou não numérica. Resultado: solicita correção e mantém saldo.
- **A3 — Destino não cadastrado.** Condição: local não existe. Resultado: solicita local válido ou cadastro do local.
- **A4 — Cancelamento/falha.** Condição: usuário cancela ou sistema falha ao salvar. Resultado: entrada não é confirmada e saldo não muda.

## UC08 — Transferir peça entre locais da loja
**Atores:** Estoquista/Repositor(a), Vendedor(a)/Atendente e Gerente, conforme permissões. **Objetivo:** movimentar unidades entre locais sem alterar o total da variação.

**Principal:** 1. Usuário abre transferência. 2. Seleciona produto/variação. 3. Define origem, destino e quantidade. 4. Sistema valida locais diferentes e saldo suficiente. 5. Sistema apresenta resumo. 6. Usuário confirma. 7. Sistema reduz saldo na origem e aumenta no destino na mesma operação. 8. Atualiza histórico e confirma.

**Alternativas:**
- **A1 — Origem igual ao destino.** Condição: os dois locais são iguais. Resultado: exige destinos diferentes e não registra.
- **A2 — Saldo insuficiente.** Condição: quantidade supera saldo na origem. Resultado: informa saldo e impede confirmação.
- **A3 — Quantidade inválida.** Condição: valor vazio, zero, negativo ou não numérico. Resultado: solicita correção; saldos não mudam.
- **A4 — Local inválido.** Condição: origem ou destino não está cadastrado/ativo. Resultado: solicita escolher local válido.
- **A5 — Falha ao salvar.** Condição: erro ao registrar. Resultado: não efetiva apenas um lado da transferência; ambos os saldos permanecem inalterados.

## UC09 — Receber alerta de estoque baixo / última unidade
**Atores destinatários:** Vendedor(a)/Atendente, Estoquista/Repositor(a) e Gerente. **Objetivo:** avisar quando uma variação atingir estoque crítico.

**Principal:** 1. Uma movimentação altera o saldo. 2. O sistema compara o novo saldo com as regras de estoque crítico da loja. 3. Se a condição for atingida, gera alerta. 4. Apresenta produto, cor, tamanho, quantidade restante e locais com unidades, se houver. 5. Disponibiliza o aviso aos usuários responsáveis. 6. Usuário consulta e inicia busca ou reposição.

**Alternativas:**
- **A1 — Estoque acima do limite.** Condição: novo saldo não é crítico. Resultado: não gera alerta.
- **A2 — Limite não configurado.** Condição: loja não definiu limite além da regra explícita de última unidade. Resultado: sistema ainda sinaliza a última unidade; não inventa limite numérico.
- **A3 — Sem reposição em outro local.** Condição: alerta existe, mas não há saldo no depósito/outro local. Resultado: informa que não há reposição registrada.
- **A4 — Alerta resolvido por entrada posterior.** Condição: reposição elevou o saldo após o alerta. Resultado: mostra estado atual e não apresenta a condição crítica como ainda ativa.

## UC10 — Registrar contagem física do estoque
**Atores:** Estoquista/Repositor(a) e Gerente. **Objetivo:** registrar quantidade encontrada fisicamente por variação e local.

**Principal:** 1. Usuário abre contagem. 2. Sistema lista itens e locais a conferir. 3. Usuário seleciona variação/local. 4. Informa a quantidade contada. 5. Sistema valida. 6. Usuário confirma. 7. Sistema grava quantidade, local, data/hora e responsável. 8. Confirma registro.

**Alternativas:**
- **A1 — Quantidade inválida.** Condição: valor vazio, negativo ou não numérico. Resultado: solicita correção e não grava.
- **A2 — Item/local não identificado.** Condição: variação ou local não está cadastrado. Resultado: informa inconsistência e exige correção de cadastro/seleção.
- **A3 — Contagem interrompida.** Condição: usuário sai antes de confirmar. Resultado: não considera contagem concluída; eventual rascunho fica pendente.
- **A4 — Contagem já registrada.** Condição: existe contagem para mesmo período, local e variação. Resultado: alerta e solicita confirmação de substituição/nova contagem conforme regra da loja.

## UC11 — Realizar fechamento diário do estoque
**Ator:** Gerente. **Objetivo:** consolidar movimentações, comparar saldos e encerrar o período.

**Principal:** 1. Gerente abre fechamento e seleciona loja/período. 2. Sistema reúne abertura, entradas, saídas e transferências. 3. Recupera contagens físicas. 4. Gerente confere pendências. 5. Sistema executa UC14 (comparação). 6. Sistema executa UC15 (Score, se fórmula aprovada). 7. Apresenta resumo e divergências. 8. Gerente revisa e confirma. 9. Sistema grava o fechamento e disponibiliza resultado nos relatórios.

**Alternativas:**
- **A1 — Contagem incompleta.** Condição: faltam contagens necessárias. Resultado: lista pendências e não marca fechamento como concluído.
- **A2 — Fórmula do Score não definida.** Condição: fórmula não está aprovada/configurada. Resultado: mostra divergências e deixa Score como pendente; não inventa número.
- **A3 — Divergências encontradas.** Condição: contagem diverge do saldo. Resultado: destaca itens/locais; gerente pode solicitar recontagem ou confirmar fechamento com divergências registradas, conforme política a validar.
- **A4 — Período já fechado.** Condição: há fechamento concluído para o período. Resultado: informa e impede duplicação; reabertura depende de regra/permissão ainda a definir.
- **A5 — Cancelamento.** Condição: gerente cancela antes de confirmar. Resultado: fechamento permanece não concluído.

## UC12 — Consultar relatórios e Score de Acurácia
**Atores:** Proprietário(a), Gerente e Financeiro. **Objetivo:** acompanhar indicadores, divergências e confiabilidade do inventário.

**Principal:** 1. Usuário abre relatórios. 2. Seleciona loja e período. 3. Sistema recupera fechamentos e contagens. 4. Apresenta resumo, divergências e Score quando calculado. 5. Usuário analisa resultados.

**Alternativas:**
- **A1 — Período sem fechamento.** Condição: não existem dados consolidados. Resultado: informa ausência de dados e não exibe indicador fictício.
- **A2 — Score pendente.** Condição: fórmula não configurada ou score não calculado. Resultado: mostra pendência e apresenta outros dados disponíveis.
- **A3 — Filtro/permissão inválida.** Condição: período ou loja não permitido/inválido. Resultado: informa problema e solicita ajuste ou acesso autorizado.

## UC13 — Consultar histórico de movimentações
**Atores:** Gerente e Financeiro. **Objetivo:** rastrear entradas, saídas, transferências e demais movimentações.

**Principal:** 1. Usuário abre histórico. 2. Define filtros por período, produto, tipo ou usuário. 3. Sistema pesquisa. 4. Exibe tipo de operação, produto/variação, quantidade, origem/destino quando aplicável, data/hora e responsável. 5. Usuário consulta os detalhes.

**Alternativas:**
- **A1 — Nenhum registro encontrado.** Condição: filtros não correspondem a movimentações. Resultado: informa ausência de resultados e permite alterar filtros.
- **A2 — Filtro inválido.** Condição: parâmetros de pesquisa inconsistentes. Resultado: solicita correção.
- **A3 — Acesso não autorizado.** Condição: perfil não tem permissão para histórico. Resultado: nega consulta e informa necessidade de autorização.

## UC14 — Comparar saldo registrado com contagem física
**Tipo:** comportamento incluído no UC11. **Ator iniciador:** Gerente, por meio do fechamento. **Objetivo:** identificar diferenças entre saldo do sistema e contagem real.

**Principal:** 1. UC11 aciona a comparação. 2. Sistema recupera saldo por produto, variação e local. 3. Recupera contagem física correspondente. 4. Compara valores. 5. Identifica combinações iguais e divergentes. 6. Apresenta resultado ao fechamento.

**Alternativas:**
- **A1 — Contagem ausente.** Condição: não existe contagem para uma combinação. Resultado: marca como pendente e informa UC11.
- **A2 — Dados incompatíveis.** Condição: contagem não corresponde a variação/local válido. Resultado: sinaliza inconsistência e não calcula divergência daquela combinação.
- **A3 — Divergência encontrada.** Condição: quantidade contada difere do saldo. Resultado: exibe diferença para investigação; não ajusta estoque automaticamente sem operação autorizada.

## UC15 — Calcular Score de Acurácia
**Tipo:** comportamento incluído no UC11. **Ator iniciador:** Gerente, por meio do fechamento. **Objetivo:** calcular indicador usando fórmula aprovada.

**Principal:** 1. UC11 aciona o cálculo após a comparação. 2. Sistema verifica fórmula aprovada e configurada. 3. Recupera dados de contagem e divergência. 4. Aplica a fórmula. 5. Associa o resultado à loja/período. 6. Exibe Score no fechamento e nos relatórios.

**Alternativas:**
- **A1 — Fórmula não configurada.** Condição: não há fórmula aprovada. Resultado: não calcula número; marca Score como pendente de definição.
- **A2 — Dados insuficientes.** Condição: faltam contagens ou valores necessários. Resultado: lista pendências e não apresenta score definitivo.
- **A3 — Erro de cálculo.** Condição: ocorre falha no processamento. Resultado: registra erro, descarta resultado parcial e sinaliza necessidade de nova tentativa.

## 4. Distribuição da descrição completa entre alunos

A orientação da atividade pede que **cada aluno descreva integralmente um único caso de uso**. O catálogo e os cenários acima cobrem o sistema; a descrição integral do UC06 — Registrar venda ou saída de peça — está em [Descrição dos Casos de Uso](Descricao_Casos_de_Uso_Controle_Estoque.md).

Casos maiores que podem ser distribuídos sem duplicação:
- UC03 — Registrar estoque inicial.
- UC04/UC05 — Consultar disponibilidade e localização (somente juntar se o professor aceitar como um único objetivo).
- UC06 — Registrar venda ou saída.
- UC08 — Transferir peça entre locais.
- UC10 — Registrar contagem física.
- UC11 — Realizar fechamento diário.

Cada aluno deve escolher apenas um caso e detalhá-lo com objetivo, atores, gatilho, pré-condições, pós-condições, fluxo principal e alternativas. O número de casos integralmente detalhados deverá corresponder ao número de alunos do grupo.

## 5. Decisões ainda pendentes

- Permissões específicas de cada perfil.
- Registro manual de vendas ou integração com PDV.
- Limite de estoque baixo além do alerta de última unidade.
- Fórmula matemática do Score de Acurácia.
- Regras para reabrir fechamento e substituir contagens.
- Tratamento de falha de conexão no aplicativo mobile.

Os itens acima são decisões a validar; não são funcionalidades confirmadas na proposta original.
