# Modelando-Sistema-Bancario-POO-Desafio-DIO
Definindo a classe Cliente
class Cliente:
    def __init__(self, nome, cpf):
        self.nome = nome
        self.cpf = cpf
Definindo a classe ContaBancaria
class ContaBancaria:
    def __init__(self, cliente, numero, saldo=0):
        self.cliente = cliente
        self.numero = numero
        self.saldo = saldo
    
    def depositar(self, valor):
        self.saldo += valor
        print(f'Depósito de R${valor} realizado. Novo saldo: R${self.saldo:.2f}')
    
    def sacar(self, valor):
        if self.saldo >= valor:
            self.saldo -= valor
            print(f'Saque de R${valor} realizado. Novo saldo: R${self.saldo:.2f}')
        else:
            print('Saldo insuficiente para saque.')
    
    def transferir(self, destino, valor):
        if self.saldo >= valor:
            self.saldo -= valor
            destino.saldo += valor
            print(f'Transferência de R${valor} realizada para conta {destino.numero}.')
            print(f'Seu novo saldo: R${self.saldo:.2f}')
        else:
            print('Saldo insuficiente para transferência.')
 Definindo a classe Transacao (opcional, dependendo da complexidade do sistema)
 class Transacao:
    def __init__(self, origem, destino, valor):
        self.origem = origem
        self.destino = destino
        self.valor = valor
    
    def executar(self):
        if self.origem.saldo >= self.valor:
            self.origem.saldo -= self.valor
            self.destino.saldo += self.valor
            print(f'Transferência de R${self.valor} realizada de {self.origem.numero} para {self.destino.numero}.')
            print(f'Saldo da conta {self.origem.numero}: R${self.origem.saldo:.2f}')
        else:
            print('Saldo insuficiente para transferência.')
Definindo a classe Banco (opcional, dependendo da complexidade do sistema)
class Banco:
    def __init__(self, nome):
        self.nome = nome
        self.contas = {}
    
    def abrir_conta(self, cliente):
        numero = len(self.contas) + 1
        conta = ContaBancaria(cliente, numero)
        self.contas[numero] = conta
        print(f'Conta aberta para {cliente.nome} com número {numero}.')
        return conta
    
    def buscar_conta(self, numero):
        if numero in self.contas:
            return self.contas[numero]
        else:
            print(f'Conta com número {numero} não encontrada.')
            return None
Exemplo de Uso:
Aqui está um exemplo simples de como usar essas classes:
# Criando um cliente
joao = Cliente('João', '123.456.789-00')

# Criando um banco
meu_banco = Banco('Meu Banco')

# Abrindo uma conta para o cliente João
conta_joao = meu_banco.abrir_conta(joao)

# Realizando operações na conta
conta_joao.depositar(1000)
conta_joao.sacar(500)

# Criando outro cliente
maria = Cliente('Maria', '987.654.321-00')

# Abrindo uma conta para a cliente Maria
conta_maria = meu_banco.abrir_conta(maria)

# Transferindo dinheiro de João para Maria
conta_joao.transferir(conta_maria, 200)

# Mostrando o saldo final das contas
print(f'Saldo final da conta de {joao.nome}: R${conta_joao.saldo:.2f}')
print(f'Saldo final da conta de {maria.nome}: R${conta_maria.saldo:.2f}')
Neste exemplo, criamos clientes (Cliente), contas bancárias (ContaBancaria), e um banco (Banco). Utilizamos métodos como depositar, sacar, transferir para realizar operações em contas bancárias. A classe Transacao e Banco são opcionais e podem ser incorporadas dependendo da complexidade e dos requisitos do sistema bancário que formos modelar.
