# Projet java
import java.awt.datatransfer.StringSelection;
import java.sql.*;
import java.util.ArrayList;

//TIP To <b>Run</b> code, press <shortcut actionId="Run"/> or
// click the <icon src="AllIcons.Actions.Execute"/> icon in the gutter.
public class Main {
    public static void main(String[] args) {//TIP Press <shortcut actionId="ShowIntentionActions"/> with your caret at the highlighted text
        // to see how IntelliJ IDEA suggests fixing it.
        String url = "jdbc:mysql://mysql-l2miashnancy.alwaysdata.net";
        String login = "381439", mdp = "Cyborgne090704!";
        String databasename = "l2miashnancy_films";
        String port = "3306";
        Connection con = null;
        try {
            Class.forName("com.mysql.cj.jdbc.Driver").getDeclaredConstructor().newInstance();
            String temp = url + ":" + port + "/" + databasename;
            con = DriverManager.getConnection(temp, login, mdp);
            System.out.println("Database connection established.");
            Statement stmt = con.createStatement();
            String requete = "SELECT titre FROM Film";
            ResultSet rs = stmt.executeQuery(requete);
            ArrayList<String> reponses = new ArrayList<>();
            System.out.println(requete);
            while(rs.next()){
                reponses.add(rs.getString("titre"));
            }
            System.out.println(reponses);
        } catch (Exception e) {
            System.out.print("Erreur inattendue");
        } finally {
            if (con != null)
                try {
                    con.close();
                }catch (Exception e){
                    System.out.println("Erreur lors de la déconnexion");
                }
        }
    }
}