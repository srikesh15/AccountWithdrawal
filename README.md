# AccountWithdrawal 
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;
     
     public class AccountWithdrawal{
        
        
            static final String url = "jdbc:mysql://localhost:3000/your_database";
            static final String username = "your_username";
            static final String password = "your_password";
            public static void main(String[] args) throws SQLException{
                
                int accountNumber=123456;
                double WithdrawalAmount=100.0;
                try(Connection connection = DriverManager.getConnection(url,username,password))
                {
                    String updateQuery = "UPDATE accounts SET balance = balance - ? WHERE account_number = ?";
                    try(PreparedStatement preparedStatement = connection.prepareStatement(updateQuery))
                    {
                    preparedStatement.setDouble(1,WithdrawalAmount);
                    preparedStatement.setInt(2,accountNumber);
                    int rowsaffected = preparedStatement.executeUpdate();
                    if(rowsaffected>0)
                        System.out.println("withdrawal suucessfully updated" + rowsaffected + "row(s)");
                    else
                        System.out.println("withdrawal failed.Account not found (or) Insufficient balance");
                    }   
                
                 catch(SQLException e){
                e.printStackTrace();
            }
        }
    }
}
            
            
           
                 
            
            


        

     
