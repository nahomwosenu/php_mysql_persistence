# Mysql DATABASE WRAPPER (PHP Simple Persistence Helper)
## Installation
 I made it really really simple to install this code in your project,
 you just need to include the Persit.php file in your code as follows

 <?php
  require_once "Persist.php";
  ?>
## Usage
 Make sure to configure the mysql username, password, database name and server address according to your environment.
 You can make those changes on lines 5-8 of Persist.php file.
 
 Let's see how to use the Persist.php file in real example.
```php
 <?php
 	require_once "Persist.php";
 	class Student{
 		var $id;//assumed to be auto-incremented, unique field on database table
 		var $name;//variable name should match the field name on the database table
 		var $age;//variable name should match the field name on the database table
 		var $sex;//variable name should match the field name on the database table
 		function __construct(){}//empty constructor, you can put your code here if needed
 		static function create($name,$age,sex){//this method will create a student instance and persist to database, returns the instance
 			$student=new Student();//create a new empty student instance
 			$student->name=$name;//assign the passed parameters to the instance
 			$student->age=$age;
 			$student->sex=$sex;
 			$student->id=Persist::save($student,"student");//persist the instance to your mysql database, first param is the instance variable and second param is the table name which it resides on the database.
 			return $student;//return the new instance
 		}
 		static function parse($query){//parses the given query and returns a list of "Student" instances if found
 			$result=Persist::executeQuery($query);//executes the query and returns a result set
 			$list=array();//empty array to temporarily store the new values
 			for($i=0;$i<count($result);$i++){
 				$student=new Student();
 				$student->name=$result[$i]['name'];//copy the column values to matching fields for current row
 				$student->age=$result[$i]['age'];
 				$student->sex=$result[$i]['sex'];
 				$list[$i]=$student;//add the current instance to the list
 			}
 			return $list;//return the list
 		}
 	}
 ?>
 ```
 ### additionally
 to update a field you can call:
 ```php
  Persist::update($instance_var,"table_name");
  ```
 to check if a specific value exists
 ```php
  Persist::exists($key,$value,$entity); where $key is the column, $value is the specific value and $entity is the name of the table
  ```
 # About Me
  Follow me on instagram: nahom_alphag33k <br/>
  Hire me on Upwork: [https://upwork.com/fl/nahometete]
