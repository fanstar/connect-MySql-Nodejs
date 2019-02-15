### Connect nMySQL + Handle Error (Node js)

```Node JS
var mysql = require('mysql');
var db_config = {
                        host: "localhost",
                        user: "user",
                        password: "pass",
                        database: "dbname"
                };

var con;

function  handleDisconnect(){
        con = mysql.createConnection(db_config);
        con.connect(function(err) {
                //if (err) throw err;
                if(err){
                        console.log("Connected Error: " + err);

                }else{
                        console.log("Connected!");
                }
        });

        con.on('error', function(err){
                console.log("On Error: " + err);

                if(err.code === 'PROTOCOL_CONNECTION_LOST') { // Connection to the MySQL server is usually
                         handleDisconnect();                         // lost due to either server restart, or a
                } else {                                      // connnection idle timeout (the wait_timeout
                //throw err;                                  // server variable configures this)
                }
        });
}


//START MY SQL
 handleDisconnect();
 
```
