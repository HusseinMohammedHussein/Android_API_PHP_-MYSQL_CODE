# Android_API_PHP_-MYSQL_CODE

### - TRY With `fetch_assoc()` 

  ```php
      <?php
        require_once 'databaseconfig.php';
        
             $user ="SELECT * FROM createUser;";
             $result = $con->query($user);
             if($result->num_rows > 0){
                     while($row = $result->fetch_assoc()) {
                            echo "id: " . $row["id"].
                                    "<br>".
                                    " - Name: " . $row["username"].
                                    "<br>".
                                    " - Email:  " . $row["email"].
                                    "<br>".
                                    " - Phone: " . $row["phone"].
                                    "<br>".
                                    " - image: "  . $row["image"].
                                    "<br>";
                      }
             }else {
                  echo "0 results";
             }
          $con->close();
       ?>             
   ```                 
   
### - TRY with `fetch()`  and `bind_result()`
    
   ```php
        <?php
          require_once 'databaseconfig.php';
            
              //creating a query
              $user = $con->prepare("SELECT * FROM createUser;");

              //executing the query
              $user->execute();

              //binding results to the query
              $user->bind_result($id, $username, $email, $phone, $image);

              $data = array();

              //traversing through all the result
              while($user->fetch()){
                $temp = array();
                $temp['id'] = $id;
                $temp['username'] = $username;
                $temp['email'] = $email;
                $temp['password'] = $password;
                $temp['phone'] = $phone;
                array_push($data, $temp);
              }

              //displaying the result in json format
              echo json_encode($data);

        ?>                   
   ```      
### - TRY With `mysqli_fetch_assoc()`    
```php
      <?php
        header("Content-type:application/json");
        require_once 'databaseconfig.php';
        $query = mysqli_query($con, "SELECT * FROM createUser;");

        $response= array();

          while($row = mysqli_fetch_assoc($query)){
                  'id'        ->$row['id'].
                  'username'  ->$row['username'].
                  'email'     ->$row['email'].
                  'password'  ->$row['password'].
                  'phone'     ->$row['phone'];
          }
          echo json_encode($response);
          $con->close();
      ?>             
   ```      
### - TRY With `$_SERVER["REQUEST_METHOD"] == "GET"`
```php
      <?php
        error_reporting(0);
          
          if ($_SERVER[‘REQUEST_METHOD’] == ‘GET’) {
          
          include('databaseconfig.php');
          
          if (isset($_GET[‘id’]) && 
              isset($_GET[‘username’]) && 
              isset($_GET[‘email’]) && 
              isset($_GET[‘password’]) && 
              isset($_GET[‘phone’])){
      
                  $id = $_GET[‘id’];
                  $username = $_GET[‘username’];
                  $email = $_GET[‘email’];
                  $password = $_GET[‘password’];
                  $phone = $_GET[‘phone’];
                  
                  $query = "SELECT * FROM createUser;";
                  $result = mysqli_query($con, $query);
                  $data = mysqli_num_rows($result);
                      
                      if($data>0) {
                            $error=”ok”;
                            echo json_encode(array(“response”=>$error,”name”=>$username));
                      }else {
                            $error = “failed”;
                            echo json_encode(array(“response”=>$error));
                      }
            }
          }
      mysqli_close($con);
   ?>      
   ```   
