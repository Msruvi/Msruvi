# Library Management System

This is a group project developed for Enterprise Architecture. The project aims to develop a library management system to efficiently manage books details.

## Group Members

- KEG/IT/2021/F/0033 - Hirumi Umeha
- KEG/IT/2021/F/0038 - Nethmi Aloka
- KEG/IT/2021/F/0092 - Ruvini Nandasena


## Tools Used

- **Java:** Primary programming language utilized for the application logic.
- **NetBeans:** Integrated Development Environment (IDE) employed for Java development.
- **Java Swing:** Toolkit utilized for constructing graphical user interfaces in Java.
- **XAMPP & MySQL:** Relational database management system used for storing book data.



## Features

- **Add Books:** Ability to add new books to the library catalog.
- **View Books:** Display existing books in the library catalog.
- **Update Books:** Modify information of existing books in the catalog.
- **Delete Books:** Remove books from the library catalog.
- **GUI:** User-friendly graphical user interface for easy navigation and interaction.

## Database and Add by **KEG/IT/2021/F/0038 - Nethmi Aloka**

- Set up MySQL database with appropriate tables for storing book details.
- Implement database connections and queries to interact with the database.


**database**    
```       
      package assignment;

import java.sql.Connection;
import java.sql.DriverManager;

/**
 *
 * @author hndit2
 */
public class database {
    
    
    public static Connection connection(){
    
        
        try{
        
            Class.forName("com.mysql.jdbc.Driver");
            Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/library","root","");
            return con;
        
        }catch(Exception e){
            System.out.println(e);
            return null;
        }
        
    }
}
```
**Add**
```
 private void jButton2ActionPerformed(java.awt.event.ActionEvent evt) {//GEN-FIRST:event_jButton2ActionPerformed
       
        Connection con = database.connection();
        
        try{
            
            PreparedStatement ptst = con.prepareStatement("insert into book (id,name,author) values(?,?,?)");
            ptst.setString(1, txtId.getText());
            ptst.setString(2, txtName.getText());
            ptst.setString(3, txtAuthor.getText());
          
            
            int i = ptst.executeUpdate();
            
            if(i != 0){
                JOptionPane.showMessageDialog(null, "Book Added Successfully !");
                clear();
            }
        
        }catch(Exception e){
            System.out.println(e);
        }
```
## Update and View Parts by **KEG/IT/2021/F/0092 - Ruvini Nandasena**

- Implement functionality to update book information.
- Implement functionality to view book details.

**Upadate**
```
private void jButton3ActionPerformed(java.awt.event.ActionEvent evt) {//GEN-FIRST:event_jButton3ActionPerformed
Connection con = database.connection();

        try{
            
            String updateqry = "update book set name = '"+txtname.getText()+"',Author = '"+txtAuthor.getText()+"' ";
            PreparedStatement ptst = con.prepareStatement(updateqry);
            
            
            int rowsA = ptst.executeUpdate();
            
           
                clear();
            

        }catch(Exception e){
            System.out.println(e);
        }

```
**View**

```
public void showData(){
    
        Connection con = database.connection();
        
        try{
        
            Statement stmt = con.createStatement();
            ResultSet rs = stmt.executeQuery("select * from book");
            
            
        DefaultTableModel model = (DefaultTableModel) view.getModel();
        model.setRowCount(0);
        
        while(rs.next()){
        
            String id = String.valueOf(rs.getString("id"));
            String name = rs.getString("name");
            String author= rs.getString("author");
          
            
            String addT [] = {id,name,author};
            
            model.addRow(addT);
        
        }
        
        }catch(Exception e){
            System.out.println(e);
        }
    }

```

## Delete and UI by **KEG/IT/2021/F/0033 - Hirumi**

- Implement functionality to delete books from the catalog.
- Design and develop the user interface for the library management system.

```
 private void jButton1ActionPerformed(java.awt.event.ActionEvent evt) {//GEN-FIRST:event_jButton1ActionPerformed
        
        Connection con = database.connection();
        
        try{
            
            Statement stmt = con.createStatement();
            int i = stmt.executeUpdate("delete from book where id = '"+Integer.parseInt(txtID.getText())+"' ");
            
            if(i!= 0){
                JOptionPane.showMessageDialog(null, "Recoard Deleted Successfully!");
                txtID.setText("");
            }
            
        
        }catch(Exception e){
            System.out.println(e);
        
        }
```

## Contribution

All group members contributed to various aspects of the project.







