# Carloca

Olá, bem vindo ao Carloca, abaixo irei explicar um pouco sobre a estrutura do banco de dados que compõe o projeto!

Primeiramente existem seis (6) tabelas, sendo elas:

# Veiculos

Que é responsável por armazenar todas as informações referentes ao veiculos, tendo os atributos:

id <br/>
id_categoria <br/>
montadora <br/>
ano_fabricacao <br/>
modelo <br/>
cor <br/>
quilometragem_atual <br/>
esta_alugado <br/>

A chave `esta_alugado` é usado para saber se o carro está em um aluguel vigente, assim, não disponibilizando-o para outro aluguel
A chave `id_categoria` referencia uma categoria, que será a próxima tabela:

# Categoria_Veiculos

Que é responsável por armazenar os dados daquela categoria, informando se é uma categoria do tipo sedan, SUV, hatch e também informar o preço da diária:

id <br/>
categoria <br/>
preco_diaria <br/>

# Clientes

Esta tabela é responsável por armazenar os dados de nosso cliente, seus atributos são:

id <br/>
cpf <br/>
cnh <br/>
nome <br/>
telefone <br/>
esta_alugando <br/>

A chave `esta_alugando` é responsável por armazenar se o cliente já está ou não alugando o carro, tendo em vista que a nossa locadora permite o aluguel de apenas um veiculo por vez

# Unidades_carloca

A nossa locadora na verdade é uma franquia, então existem varias unidades espalhadas pelo solo brasileiro, esta tabela é responsável por armazenar os endereços de cada uma, seus atributos são:

id <br/>
logradouro <br/>
bairro <br/>
cidade <br/>
estado <br/>
numero <br/>

# Alugueis

Esta é a tabela mais sensível e importante do nosso banco de dados, pois ela nos informará os dados de cada aluguel, seus atributos são

id <br/>
id_cliente <br/>
id_veiculo  <br/>
data_retirada  <br/>
data_devolucao  <br/>
diarias  <br/>
unidade_retirada  <br/>
unidade_devolucao  <br/>

A chave `id_cliente` referencia à um cliente da tabela `Clientes`, a chave `id_veiuclo` referencia à um veículo da tabela de `Veiculos`, e as chaves `unidade_retirada` e `unidade_devolucao` referenciam à endereços da tabela `Unidades_Carloca`

Nesta tabela temos quatro triggers, que são responsáveis por:

- Verificar se o carro já está sendo alugado;
- Verificar se o cliente já está alugando um carro;
- Atualizar a condição do cliente, já que ele estará alugando um carro;
- Atualizar a condição do veículo, já que ele estará mais sendo alugado.

# Devolucao

Por fim, nossa última tabela, que é responsável por informar os dados da devolucao de um véiculo, seus atributos são:

id  <br/>
id_aluguel  <br/>
data_devolucao  <br/>
quilometragem_rodada  <br/>
valor_avarias_veiculo  <br/>
diarias_excedidas  <br/>

A chave `id_aluguel` referencia a um aluguel da tebela `Alugeis`, a chave `data_devolucao` é responsável por verificar se houve diarias excedidas ou não

Nesta tabela temos três triggers, que são responsáveis por:

- Atualizar a quilometragem do carro;
- Atualizar a condição do cliente, já que ele não estará mais alugando um carro;
- Atualizar a condição do veículo, já que ele não estará mais sendo alugado.



<h1>
  Explicando os requisitos do projeto
</h1>

<h3>
  Um carro possui modelo montadora, cor e versão.
</h3>

A tabela `veiculos` contempla todos esses parâmetros

<h3>
  As cores de carro disponiveis são apenas branco, preto e prata
</h3>

Na tabela `veiculos` o campo `cor` é do tipo _ENUM_  e seus valores aceitos são branco, preto e prata

<h3>
  Existem várias categorias de veiculos (hatch, sedam compacto, sedam médio, SUV, etc...)
</h3>

A tabela `categoria` executa esta função

<h3>
  Um cliente pode alugar um carro somente na modalidade "diária"
</h3>

Todo o bacno foi modelado considerando o regime de diáirias

<h3>
  Um cliente não pode alugar mais de um carro
</h3>

Existe um trigger na tabela `alugueis` que não permite um cliente alugar mais de um carro

<h3>
  Enquanto um carro estiver locado por um cliente não pode ser ofetado para outro
</h3>

Existe um campo na tabela `veiculos` (esta_alugado) que pode ser usado como filtro na hora de buscar um veículo disponível

<h3>
   O sistema deve manter o histórico dos clientes que locaram determinado carro
</h3>

Basta fazer uma query na tabela alugueis informando o id do cliente no where

<h3>
   O sistema deve manter o histórico de quantos quilometros o cliente rodou com o carro bemm como a quilometragem atual de cada um dos carros.
</h3>

O hisórico de quantos quilometros o cliente rodou pode ser feito na tabela devolução, fazendo um join na tabela alugueis, informando o id do cliente no where.
E a quilometragem atual dos veículos está contemplada na tabela de veiculos

<h3>
   Existem várias unidades da fraquia CARLOCA o sistema deve saber onde o carro foi locado e onde foi devolvido cada veiculo
</h3>

Existe a tabela `unidades_carloca` que armazena os endereçois das franquias e na tabela `alugueis` existe o coluna `unidade_devolucao` e `unidade_retirada`que é em qual unidade o carro foi locado e em qual ele será devolvido
