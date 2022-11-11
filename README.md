- package Programa;

import java.util.ArrayList;
import java.util.Scanner;

public class AgenciaBancaria {
    static Scanner imput = new Scanner(System.in);
    static ArrayList<Conta> contasBancarias;

    public static void main(String[] args) {

        int reinicio = 1;

        do {

            contasBancarias = new ArrayList<Conta>();
            operacoes();

            System.out.println("Digite 1 para continuar ou 0 para sair ");
        }while (reinicio == 1);
    }

    public static void operacoes(){
        System.out.println("-------------------------------------------");
        System.out.println("----------Bem Vindos a Nossa Agência----------");
        System.out.println("-------------------------------------------");
        System.out.println("****** Selecione uma operação que deseja realizar ******");
        System.out.println("-------------------------------------------");
        System.out.println("|   Opção 1- Criar conta   |");
        System.out.println("|   Opção 2- Depositar     |");
        System.out.println("|   Opção 3- Sacar         |");
        System.out.println("|   Opção 4- Transferir    |");
        System.out.println("|   Opção 5- Listar        |");
        System.out.println("|   Opção 6- Sair          |");

        int operacao = imput.nextInt();

        switch (operacao){
            case 1:
                criarConta();
                break;

            case 2:
                depositar();
                break;

            case 3:
                sacar();
                break;

            case 4:
                tranferir();
                break;

            case 5:
                listarContas();
                break;

            case 6:
                System.out.println("Obrigado pela preferêcia");
                System.exit(0);

            default:
                System.out.println("Opção inválida!");
                operacoes();
                break;
        }
    }

    public static void criarConta(){
        System.out.println("\nNome: ");
        String nome = imput.next();

        System.out.println("\nCPF: ");
        String cpf = imput.next();

        System.out.println("\nEmail: ");
        String email = imput.next();

        Pessoa pessoa = new Pessoa(nome, cpf, email);

        Conta conta = new Conta(pessoa);

        contasBancarias.add(conta);
        System.out.println("Sua conta foi criada com sucesso!");

        operacoes();
    }

    private static Conta encontrarConta(int numeroConta){
        Conta conta = null;
        if (contasBancarias.size() > 0){
            for (Conta c: contasBancarias){
                if (c.getNumeroConta() == numeroConta);
                conta = c;
            }
        }
        return conta;
    }

    public static void depositar(){
        System.out.println("Número da conta: ");
        int numeroConta = imput.nextInt();

        Conta conta = encontrarConta(numeroConta);

        if (conta != null){
            System.out.println("Qual valor deseja depositar? ");
            Double valorDeposito = imput.nextDouble();
            conta.depositar(valorDeposito);
            System.out.println(" Valor depositado com sucesso! ");
        }else {
            System.out.println(" conta não encontrada! ");
        }
        operacoes();
    }

    public static void sacar(){
        System.out.println("Número da conta: ");
        int numeroConta = imput.nextInt();

        Conta conta = encontrarConta(numeroConta);

        if (conta != null){
            System.out.println("Qual valor deseja sacar? ");
            Double valorSaque = imput.nextDouble();
            conta.sacar(valorSaque);
            System.out.println(" Valor sacado com sucesso! ");
        }else {
            System.out.println(" conta não encontrada! ");
        }
        operacoes();
    }

    public static void tranferir(){
        System.out.println("Número da conta do remenente: ");
        int numeroContaRemenente = imput.nextInt();

        Conta contaRemetente = encontrarConta(numeroContaRemenente);

        if (contaRemetente != null){
            System.out.println("Número da conta do destinatário: ");
            int numeroContaDestinatario = imput.nextInt();

            Conta contaDestinatario = encontrarConta(numeroContaDestinatario);

            if (contaDestinatario != null){
                System.out.println("Valor da transferência: ");
                Double valor = imput.nextDouble();

                contaRemetente.transferir(contaDestinatario, valor);
            }
        }
        operacoes();
    }

    public static void listarContas(){
        if (contasBancarias.size() > 0 ){
            for (Conta conta: contasBancarias) {
                System.out.println(conta);
            }
            }else{
                System.out.println("Não há contas cadastradas! ");
            }
        operacoes();
        }
    }
