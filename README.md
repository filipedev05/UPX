package upx;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;
import java.util.Scanner;

public class SimuladorDesmatamento {

    private static void salvarSimulacao(final double areaDesmatada, final int numeroArvores, 
                                         final double areaAgricola, final double areaMadeireira, 
                                         final double areaUrbanizacao, final double impactoTotal) {
        String url = "jdbc:mysql://localhost:3306/SimuladorDesmatamentoDB";
        String user = "seu_usuario"; 
        String password = "sua_senha"; 

        String sql = "INSERT INTO Simulacoes (area_desmatada, numero_arvores, area_agricola, area_madeireira, area_urbanizacao, impacto_total) VALUES (?, ?, ?, ?, ?, ?)";

        try (Connection conn = DriverManager.getConnection(url, user, password);
             PreparedStatement pstmt = conn.prepareStatement(sql)) {
            
            pstmt.setDouble(1, areaDesmatada);
            pstmt.setInt(2, numeroArvores);
            pstmt.setDouble(3, areaAgricola);
            pstmt.setDouble(4, areaMadeireira);
            pstmt.setDouble(5, areaUrbanizacao);
            pstmt.setDouble(6, impactoTotal);
            
            pstmt.executeUpdate();
            System.out.println("Simulação salva com sucesso no banco de dados!");
        } catch (SQLException e) {
            System.out.println("Erro ao salvar a simulação: " + e.getMessage());
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Bem-vindo ao Simulador de Desmatamento!");

        System.out.print("Digite a área desmatada (em hectares): ");
        double areaDesmatada = scanner.nextDouble();

        System.out.print("Digite a quantidade de árvores derrubadas: ");
        int numeroArvores = scanner.nextInt();

        System.out.print("Digite a área utilizada para práticas agrícolas (em hectares): ");
        double areaAgricola = scanner.nextDouble();

        System.out.print("Digite a área explorada para exploração madeireira (em hectares): ");
        double areaMadeireira = scanner.nextDouble();

        System.out.print("Digite a área urbanizada (em hectares): ");
        double areaUrbanizacao = scanner.nextDouble();

        double impactoTotal = calcularImpacto(areaDesmatada, numeroArvores, areaAgricola, areaMadeireira, areaUrbanizacao);

       
        salvarSimulacao(areaDesmatada, numeroArvores, areaAgricola, areaMadeireira, areaUrbanizacao, impactoTotal);

        System.out.println("\nResultados do Simulador:");
        System.out.printf("Impacto Total do Desmatamento: %.2f pontos%n", impactoTotal);

        sugerirMinimizacaoDesmatamento();

        scanner.close();
    }

    private static void sugerirMinimizacaoDesmatamento() {
		
		
	}

	private static double calcularImpacto(double areaDesmatada, int numeroArvores, 
                                           double area, double areaMadeireira, double areaUrbanizacao) {
		return 0;
	}
}
