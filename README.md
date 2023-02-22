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

# Devolucao

Por fim, nossa última tabela, que é responsável por informar os dados da devolucao de um véiculo, seus atributos são:

id  <br/>
id_aluguel  <br/>
data_devolucao  <br/>
quilometragem_rodada  <br/>
valor_avarias_veiculo  <br/>
diarias_excedidas  <br/>

A chave `id_aluguel` referencia a um aluguel da tebela `Alugeis`, a chave `data_devolucao` é responsável por verificar se houve diarias excedidas ou não
