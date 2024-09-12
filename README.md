public class Material {
    // Atributos
    private String codigo;
    private String titulo;
    private boolean disponivel;
    
    // Membro estático para rastrear o número total de materiais
    private static int totalMateriais = 0;

    // Construtor da classe base
    public Material(String codigo, String titulo, boolean disponivel) {
        this.codigo = codigo;
        this.titulo = titulo;
        this.disponivel = disponivel;
        totalMateriais++;  // Incrementa o número de materiais a cada novo material criado
    }

    // Método estático para obter o número total de materiais
    public static int getTotalMateriais() {
        return totalMateriais;
    }

    // Método para exibir informações do material
    public void exibirInformacoes() {
        System.out.println("Código: " + codigo);
        System.out.println("Título: " + titulo);
        System.out.println("Disponível: " + (disponivel ? "Sim" : "Não"));
    }

    // Getters e Setters (opcional, caso necessário)
    public String getCodigo() {
        return codigo;
    }

    public boolean isDisponivel() {
        return disponivel;
    }
}
public class Livro extends Material {
    // Atributos adicionais
    private String autor;
    private int numPaginas;

    // Construtor
    public Livro(String codigo, String titulo, boolean disponivel, String autor, int numPaginas) {
        super(codigo, titulo, disponivel);  // Chama o construtor da classe base
        this.autor = autor;
        this.numPaginas = numPaginas;
    }

    // Sobrescrita do método para exibir informações específicas do Livro
    @Override
    public void exibirInformacoes() {
        super.exibirInformacoes();  // Exibe informações comuns
        System.out.println("Autor: " + autor);
        System.out.println("Número de Páginas: " + numPaginas);
    }
}
public class Revista extends Material {
    // Atributo adicional
    private int edicao;

    // Construtor
    public Revista(String codigo, String titulo, boolean disponivel, int edicao) {
        super(codigo, titulo, disponivel);  // Chama o construtor da classe base
        this.edicao = edicao;
    }

    // Sobrescrita do método para exibir informações específicas da Revista
    @Override
    public void exibirInformacoes() {
        super.exibirInformacoes();  // Exibe informações comuns
        System.out.println("Edição: " + edicao);
    }
}
import java.util.ArrayList;

public class Biblioteca {
    // Lista para armazenar os materiais (livros e revistas)
    private ArrayList<Material> materiais;

    // Construtor da classe Biblioteca
    public Biblioteca() {
        materiais = new ArrayList<>();
    }

    // Método para adicionar um material à biblioteca
    public void adicionarMaterial(Material material) {
        materiais.add(material);
    }

    // Método para listar todos os materiais disponíveis
    public void listarMateriaisDisponiveis() {
        for (Material material : materiais) {
            if (material.isDisponivel()) {
                material.exibirInformacoes();
                System.out.println();
            }
        }
    }

    // Método para buscar um material pelo código
    public Material buscarMaterialPorCodigo(String codigo) {
        for (Material material : materiais) {
            if (material.getCodigo().equals(codigo)) {
                return material;
            }
        }
        return null;  // Retorna null se o material não for encontrado
    }
}
public class Main {
    public static void main(String[] args) {
        // Criação da biblioteca
        Biblioteca biblioteca = new Biblioteca();

        // Adicionando materiais
        Livro livro1 = new Livro("001", "Java Programming", true, "Autor 1", 500);
        Revista revista1 = new Revista("002", "Tech Monthly", true, 12);

        biblioteca.adicionarMaterial(livro1);
        biblioteca.adicionarMaterial(revista1);

        // Listar materiais disponíveis
        System.out.println("Materiais Disponíveis:");
        biblioteca.listarMateriaisDisponiveis();

        // Buscar material por código
        System.out.println("Busca por código '001':");
        Material materialEncontrado = biblioteca.buscarMaterialPorCodigo("001");
        if (materialEncontrado != null) {
            materialEncontrado.exibirInformacoes();
        } else {
            System.out.println("Material não encontrado.");
        }

        // Exibir o total de materiais
        System.out.println("Total de materiais: " + Material.getTotalMateriais());
    }
}
