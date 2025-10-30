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



import textwrap


def menu():
    menu = """\n
    ================ MENU ================
    [d]\tDepositar
    [s]\tSacar
    [e]\tExtrato
    [nc]\tNova conta
    [lc]\tListar contas
    [nu]\tNovo usuário
    [q]\tSair
    => """
    return input(textwrap.dedent(menu))


def depositar(saldo, valor, extrato, /):
    if valor > 0:
        saldo += valor
        extrato += f"Depósito:\tR$ {valor:.2f}\n"
        print("\n=== Depósito realizado com sucesso! ===")
    else:
        print("\n@@@ Operação falhou! O valor informado é inválido. @@@")

    return saldo, extrato


def sacar(*, saldo, valor, extrato, limite, numero_saques, limite_saques):
    excedeu_saldo = valor > saldo
    excedeu_limite = valor > limite
    excedeu_saques = numero_saques >= limite_saques

    if excedeu_saldo:
        print("\n@@@ Operação falhou! Você não tem saldo suficiente. @@@")

    elif excedeu_limite:
        print("\n@@@ Operação falhou! O valor do saque excede o limite. @@@")

    elif excedeu_saques:
        print("\n@@@ Operação falhou! Número máximo de saques excedido. @@@")

    elif valor > 0:
        saldo -= valor
        extrato += f"Saque:\t\tR$ {valor:.2f}\n"
        numero_saques += 1
        print("\n=== Saque realizado com sucesso! ===")

    else:
        print("\n@@@ Operação falhou! O valor informado é inválido. @@@")

    return saldo, extrato


def exibir_extrato(saldo, /, *, extrato):
    print("\n================ EXTRATO ================")
    print("Não foram realizadas movimentações." if not extrato else extrato)
    print(f"\nSaldo:\t\tR$ {saldo:.2f}")
    print("==========================================")


def criar_usuario(usuarios):
    cpf = input("Informe o CPF (somente número): ")
    usuario = filtrar_usuario(cpf, usuarios)

    if usuario:
        print("\n@@@ Já existe usuário com esse CPF! @@@")
        return

    nome = input("Informe o nome completo: ")
    data_nascimento = input("Informe a data de nascimento (dd-mm-aaaa): ")
    endereco = input("Informe o endereço (logradouro, nro - bairro - cidade/sigla estado): ")

    usuarios.append({"nome": nome, "data_nascimento": data_nascimento, "cpf": cpf, "endereco": endereco})

    print("=== Usuário criado com sucesso! ===")


def filtrar_usuario(cpf, usuarios):
    usuarios_filtrados = [usuario for usuario in usuarios if usuario["cpf"] == cpf]
    return usuarios_filtrados[0] if usuarios_filtrados else None


def criar_conta(agencia, numero_conta, usuarios):
    cpf = input("Informe o CPF do usuário: ")
    usuario = filtrar_usuario(cpf, usuarios)

    if usuario:
        print("\n=== Conta criada com sucesso! ===")
        return {"agencia": agencia, "numero_conta": numero_conta, "usuario": usuario}

    print("\n@@@ Usuário não encontrado, fluxo de criação de conta encerrado! @@@")


def listar_contas(contas):
    for conta in contas:
        linha = f"""\
            Agência:\t{conta['agencia']}
            C/C:\t\t{conta['numero_conta']}
            Titular:\t{conta['usuario']['nome']}
        """
        print("=" * 100)
        print(textwrap.dedent(linha))


def main():
    LIMITE_SAQUES = 3
    AGENCIA = "0001"

    saldo = 0
    limite = 500
    extrato = ""
    numero_saques = 0
    usuarios = []
    contas = []

    while True:
        opcao = menu()

        if opcao == "d":
            valor = float(input("Informe o valor do depósito: "))

            saldo, extrato = depositar(saldo, valor, extrato)

        elif opcao == "s":
            valor = float(input("Informe o valor do saque: "))

            saldo, extrato = sacar(
                saldo=saldo,
                valor=valor,
                extrato=extrato,
                limite=limite,
                numero_saques=numero_saques,
                limite_saques=LIMITE_SAQUES,
            )

        elif opcao == "e":
            exibir_extrato(saldo, extrato=extrato)

        elif opcao == "nu":
            criar_usuario(usuarios)

        elif opcao == "nc":
            numero_conta = len(contas) + 1
            conta = criar_conta(AGENCIA, numero_conta, usuarios)

            if conta:
                contas.append(conta)

        elif opcao == "lc":
            listar_contas(contas)

        elif opcao == "q":
            break

        else:
            print("Operação inválida, por favor selecione novamente a operação desejada.")


main()

 
