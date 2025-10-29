# -Criando-um-Sistema-Bancario-com-Python-


# 🏦 Sistema Bancário Simples em Python

Este é um **sistema bancário simples** desenvolvido em Python, que permite ao usuário realizar operações básicas de conta corrente, como **depósitos, saques e consulta de extrato**. O projeto é ideal para iniciantes que querem praticar lógica de programação, estruturas de controle e manipulação de strings.

---

## 💻 Funcionalidades

- **Depósito**: Permite adicionar saldo à conta.  
- **Saque**: Permite retirar dinheiro respeitando:
  - Saldo disponível
  - Limite máximo por saque (R$ 500)
  - Número máximo de saques diários (3 saques)
- **Extrato**: Exibe todas as transações realizadas, incluindo depósitos e saques.  
- **Sair**: Finaliza a execução do programa.

---

## 📝 Regras do Sistema

1. O **saldo inicial** é R$ 0,00.  
2. O **limite de saque por operação** é R$ 500,00.  
3. É permitido **no máximo 3 saques** por execução do programa.  
4. Valores inválidos (negativos ou zero) não são aceitos.  
5. As transações ficam registradas no **extrato**, que pode ser consultado a qualquer momento.

---

## ⚙️ Como Usar

1. Clone este repositório ou copie o código para o seu ambiente local.  
2. Execute o script em Python (versão 3.x recomendada):  
   
   python banco.py
Siga o menu interativo exibido no terminal:

Copiar código
[1] Depositar
[2] Sacar
[3] Extrato
[4] Sair
=> 
Insira os valores conforme solicitado e acompanhe seu saldo e extrato.

🖼️ Exemplo de Execução
ruby
Copiar código
=> [1] Depositar
Informe o valor do depósito: 1000
=> [2] Sacar
Informe o valor do saque: 200
=> [3] Extrato
================ EXTRATO ================
Depósito: R$ 1000.00
Saque: R$ 200.00

Saldo: R$ 800.00
==========================================
=> [4] Sair
📚 Tecnologias Utilizadas
Python 3.x

Estruturas de controle: if, elif, else

Laços de repetição: while

Manipulação de strings e formatação de valores monetários

🔧 Melhorias Futuras
Adicionar persistência de dados (salvar extrato em arquivo).

Permitir múltiplas contas com login de usuário.

Implementar interface gráfica com Tkinter ou PySimpleGUI.

 
