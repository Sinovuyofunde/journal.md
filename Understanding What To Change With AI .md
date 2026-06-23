Improved Java Code (Readable & Professional Version)

import java.util.ArrayList;
import java.util.List;

class UserManager

private List<User> userList;  
private DBConn database;  

public UserManager(DBConn databaseConnection)  
    this.database = databaseConnection;  
    this.userList = new ArrayList<>();  

public boolean registerUser(String username, String password, String email)  

    // Validate input  
    if (username.length() < 3 || password.length() < 8 || !email.contains("@"))  
        return false;  

    // Check for duplicate username  
    for (User user : userList)  
        if (user.getUsername().equals(username))  
            return false;  

    // Create new user object  
    User newUser = new User(username, password, email);  
    userList.add(newUser);  

    // Save user to database  
    boolean result = database.execute(  
        "INSERT INTO users VALUES ('" + username + "', '" + password + "', '" + email + "')"  
    );  

    return result;  

public User getUser(String username)  

    for (User user : userList)  
        if (user.getUsername().equals(username))  
            return user;  

    return null;  
class User

private String username;  
private String password;  
private String email;  

public User(String username, String password, String email)  
    this.username = username;  
    this.password = password;  
    this.email = email;  

public String getUsername()  
    return username  

public String getPassword()  
    return password  

public String getEmail()  
    return email
