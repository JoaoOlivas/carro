CLASSE DO CARRO

public class Carro {
    private String cor;
    private String marca;
    private int ano;
    private double preco;

    public Carro(String cor, String marca, int ano, double preco) {
        this.cor = cor;
        this.marca = marca;
        this.ano = ano;
        this.preco = preco;
    }

    // Getters e Setters
    public String getCor() {
        return cor;
    }

    public void setCor(String cor) {
        this.cor = cor;
    }

    public String getMarca() {
        return marca;
    }

    public void setMarca(String marca) {
        this.marca = marca;
    }

    public int getAno() {
        return ano;
    }

    public void setAno(int ano) {
        this.ano = ano;
    }

    public double getPreco() {
        return preco;
    }

    public void setPreco(double preco) {
        this.preco = preco;
    }

    @Override
    public String toString() {
        return "Carro{" +
                "cor='" + cor + '\'' +
                ", marca='" + marca + '\'' +
                ", ano=" + ano +
                ", preco=" + preco +
                '}';
    }
}


CLASSE VETOR CARRO

import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

public class VetorCarros {
    private List<Carro> carros;

    public VetorCarros() {
        this.carros = new ArrayList<>();
    }

    // Adicionar um carro
    public void adicionarCarro(Carro carro) {
        carros.add(carro);
    }

    // Remover um carro pelo atributo
    public boolean removerCarroPorAtributo(String atributo, String valor) {
        Iterator<Carro> iterator = carros.iterator();
        while (iterator.hasNext()) {
            Carro carro = iterator.next();
            switch (atributo.toLowerCase()) {
                case "cor":
                    if (carro.getCor().equalsIgnoreCase(valor)) {
                        iterator.remove();
                        return true;
                    }
                    break;
                case "marca":
                    if (carro.getMarca().equalsIgnoreCase(valor)) {
                        iterator.remove();
                        return true;
                    }
                    break;
                case "ano":
                    if (Integer.toString(carro.getAno()).equals(valor)) {
                        iterator.remove();
                        return true;
                    }
                    break;
                case "preco":
                    if (Double.toString(carro.getPreco()).equals(valor)) {
                        iterator.remove();
                        return true;
                    }
                    break;
            }
        }
        return false;
    }

    // Contar carros com determinado atributo
    public int contarCarrosPorAtributo(String atributo, String valor) {
        int count = 0;
        for (Carro carro : carros) {
            switch (atributo.toLowerCase()) {
                case "cor":
                    if (carro.getCor().equalsIgnoreCase(valor)) {
                        count++;
                    }
                    break;
                case "marca":
                    if (carro.getMarca().equalsIgnoreCase(valor)) {
                        count++;
                    }
                    break;
                case "ano":
                    if (Integer.toString(carro.getAno()).equals(valor)) {
                        count++;
                    }
                    break;
                case "preco":
                    if (Double.toString(carro.getPreco()).equals(valor)) {
                        count++;
                    }
                    break;
            }
        }
        return count;
    }

    // Exibir todos os carros
    public void exibirCarros() {
        for (Carro carro : carros) {
            System.out.println(carro);
        }
    }
}


CLASSE APLICAÇÃO

import java.util.Scanner;

public class Aplicacao {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        VetorCarros vetorCarros = new VetorCarros();
        
        while (true) {
            System.out.println("\nMenu:");
            System.out.println("1. Adicionar um carro no vetor");
            System.out.println("2. Remover um carro do vetor");
            System.out.println("3. Quantidade de carros com determinado atributo");
            System.out.println("4. Exibir todos os carros");
            System.out.println("5. Sair");
            System.out.print("Escolha uma opção: ");
            int opcao = scanner.nextInt();
            scanner.nextLine(); // Consumir nova linha

            switch (opcao) {
                case 1:
                    System.out.print("Digite a cor do carro: ");
                    String cor = scanner.nextLine();
                    System.out.print("Digite a marca do carro: ");
                    String marca = scanner.nextLine();
                    System.out.print("Digite o ano do carro: ");
                    int ano = scanner.nextInt();
                    System.out.print("Digite o preço do carro: ");
                    double preco = scanner.nextDouble();
                    vetorCarros.adicionarCarro(new Carro(cor, marca, ano, preco));
                    break;

                case 2:
                    System.out.print("Escolha o atributo para remoção (cor, marca, ano, preco): ");
                    String atributoRemover = scanner.nextLine();
                    System.out.print("Digite o valor do atributo: ");
                    String valorRemover = scanner.nextLine();
                    if (vetorCarros.removerCarroPorAtributo(atributoRemover, valorRemover)) {
                        System.out.println("Carro removido com sucesso.");
                    } else {
                        System.out.println("Nenhum carro encontrado com esse atributo.");
                    }
                    break;

                case 3:
                    System.out.print("Escolha o atributo para contagem (cor, marca, ano, preco): ");
                    String atributoContar = scanner.nextLine();
                    System.out.print("Digite o valor do atributo: ");
                    String valorContar = scanner.nextLine();
                    int quantidade = vetorCarros.contarCarrosPorAtributo(atributoContar, valorContar);
                    System.out.println("Quantidade de carros com o atributo " + atributoContar + " = " + valorContar + ": " + quantidade);
                    break;

                case 4:
                    vetorCarros.exibirCarros();
                    break;

                case 5:
                    System.out.println("Saindo...");
                    scanner.close();
                    return;

                default:
                    System.out.println("Opção inválida.");
                    break;
            }
        }
    }
}
