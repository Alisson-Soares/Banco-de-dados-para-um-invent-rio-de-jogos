# Banco de dados para jogos

Tarefas a serem feitas

Tarefa ID: TSK-001
Tipo: Regra de Negócio (RN01 - Validação de Troca)
Descrição: Para que o método validateTrade() da classe Trade retorne true, duas condições obrigatórias devem ser atendidas: o comprador deve ter saldo suficiente (value na classe Money) para cobrir o totalPrice, e o vendedor deve possuir os itens listados na transação dentro de sua lista de slots no Inventory.
Testes:
 * Teste 1: Iniciar troca onde o comprador tem dinheiro suficiente e o vendedor tem os itens (Esperado: validateTrade() = true).
 * Teste 2: Iniciar troca onde o comprador não tem dinheiro suficiente (Esperado: validateTrade() = false).
 * Teste 3: Iniciar troca onde o vendedor não possui os itens no inventário (Esperado: validateTrade() = false).
Tarefa ID: TSK-002
Tipo: Caso de Uso (UC01 - Executar Troca)
Descrição: Quando uma troca é validada, o sistema aciona o executeTrade(). O sistema deve remover a lista de itens (List<Item>) do Inventory do vendedor e adicioná-la ao Inventory do comprador. Simultaneamente, deve usar SubtractValue() no Money do comprador e AddValue() no Money do vendedor utilizando o totalPrice. Ao final, a variável isCompleted deve ser marcada como true.
Testes:
 * Teste 1: Verificar se os itens saíram do inventário do vendedor.
 * Teste 2: Verificar se os itens entraram no inventário do comprador.
 * Teste 3: Verificar se o saldo (Money) de ambas as entidades foi atualizado corretamente (soma e subtração do totalPrice).
 * Teste 4: Verificar se isCompleted da classe Trade mudou para true.
Tarefa ID: TSK-003
Tipo: História de Usuário (US01 - Cancelamento de Transação)
Descrição: Como jogador (Player), quero poder cancelar uma negociação em andamento (cancelTrade()) antes que ela seja executada, para que eu possa desistir da compra ou venda sem perder meus itens ou dinheiro.
Testes:
 * Teste 1: Acionar cancelTrade() após instanciar a troca, mas antes do executeTrade(). (Esperado: Nenhum item ou dinheiro é transferido).
 * Teste 2: Verificar se isCompleted permanece false após o cancelamento.
Tarefa ID: TSK-004
Tipo: Regra de Negócio (RN02 - Restrição de Interesses de NPC)
Descrição: O NPC possui o método GetInterests(). Durante a configuração de uma troca (Trade), caso o jogador esteja vendendo itens para o NPC, o sistema deve validar se o Item oferecido faz parte da lista de interesses do NPC. Se não fizer, a troca não pode ser iniciada ou validada.
Testes:
 * Teste 1: Jogador tenta vender um item presente no retorno de GetInterests() do NPC (Esperado: Troca permitida).
 * Teste 2: Jogador tenta vender um item que NÃO está na lista de interesses do NPC (Esperado: Troca bloqueada/inválida).
Tarefa ID: TSK-005
Tipo: Regra de Negócio (RN03 - Conversão de Moedas)
Descrição: O sistema deve lidar com diferentes tipos de moedas do enumeration Coin (GOLD, SILVER, BRONZE). Quando houver transações ou cálculos de totalPrice que envolvam moedas diferentes, o sistema deve utilizar o método ConversionType(Money) da classe Money para padronizar os valores antes de efetuar adições ou subtrações (BigDecimal).
Testes:
 * Teste 1: Somar valores onde o item custa SILVER e o jogador paga em GOLD (Esperado: O sistema converte corretamente usando ConversionType() e dá o troco correto).
 * Teste 2: Tentar pagar um item usando moedas de BRONZE equivalentes ao valor em SILVER (Esperado: Transação aprovada se o valor convertido for suficiente).
Tarefa ID: TSK-006
Tipo: História de Usuário (US02 - Busca no Inventário)
Descrição: Como jogador (Player) ou sistema controlador de NPC, preciso poder buscar itens específicos (FindItem() ou FindItem(List<Item>)) nos meus slots de inventário (Inventory), para verificar rapidamente se possuo os requisitos para uma missão ou itens para vender.
Testes:
 * Teste 1: Chamar FindItem() passando o parâmetro de um item que existe no inventário (Esperado: Retornar o objeto Item).
 * Teste 2: Chamar FindItem() passando um item que não existe (Esperado: Retornar nulo ou tratar a exceção adequadamente).
