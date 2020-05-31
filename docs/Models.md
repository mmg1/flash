## Models

  Models are classes that are designed to work with database. it manages the database, logic and rules of the web application.

### Create a model

  Let’s create the first model. Open the `app/models.php` file and put the following PHP code in it:

```php
class blog extends Models {
  private $title;
  private $author;
  private $date;

  function __construct() {
    //create database connection
    $this->connect('db');
  }

  function get_data() {

    $result = $this->db->query('select * from blog');

    //close database connection
    $this->db->close();

    return $result;
  }
}
```

### Use Database

  Create database connection in model.

```php
class blog extends Models {
  function __construct() {
    $this->connect('blog_db');
  }

  function get_data() {
    //select data from database
    $result = $this->blog_db->query('select * from blog');
    return $result;
  }

  function put_data($title,$author) {
    //insert data in database
    return $this->blog_db->query("insert into blog values('$title','$author')");
  }
}
```

### Use Model

  Use models in views to use database in your application.

```php
//Include models file
require_once('models.php');

class view extends Views{
  function home() {
    //create model object
    $blog = new blog();
    //get data from model
    foreach($blog->get_data() as $data) {
      $blog_data[] = $data;
    }
    //response data
    return $this->response($blog_data);
  }
}
```
