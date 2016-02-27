# PHP7 Introduces Two New Operators: The Combined Comparison ("Spaceship") Operator, and the Null Coalesce Operator. 

PHP 7 was released in December, 2015 after nearly two years of development, and its development team focused on speeding up the twenty year old programming language. Even though PHP is already one of the fastest, oldest, and most widely used web programming languages, they were still able to add in features while still maintaining backwards compatibility with older releases.

They accomplished this in many ways: including optimizing the Zend engine, and implementing new operators to reduce boilerplate code.  PHP 7's development team introduced two new operators to the language which will result in "ease of life" for many developers. These operators are the: Combined Comparison ("Spaceship") Operator, and the Null Coalesce Operator.   
With the addition of these operators, the developers of PHP 7 are living up to their promises of "speeding up the internet" by introducing operators that can be implemented to reduce the highly detailed level of code necessary to accomplish various tedious programming tasks.  Properly understanding the intent, and application, of each operator will be vital for any PHP developer looking to decrease development and debugging time associated with development 

## The  Combined Comparison Operator  "<=>":
The combined comparison operator, nicknamed the "spaceship" operator is aimed to help cut down on the amount of time needed to write order sorting functions.  This operator can also be found in other languages such as: Pearl, Ruby, and Groovy - but its more formal name is the "three-way comparison operator". 
Before PHP 7 was released, programmers may have used usort() to sort an array, but with the addition of the spaceship operator, usort() will require less detail code to properly function.

For a quick refresher, the syntax for usort() is: 
    usort ($array, $value_compare _func). 

parameters:
    $array = any array
    $value_compare_func: This was a user created function, that would set the behavior of how the user wanted the values to be sorted. 

The spaceship operator will be greatly beneficial for use with usort(), because it takes a lot of very detailed code to properly develop a value compare function for  usort().
Here is an example of the old way that a developer would have to write an order sorting function:
    
	function order_func($x, $y) {
    return ($x < $y) ? -1 : (($x > $y) ? 1 : 0);
    }
	
	$x = array(6,2,9,12,4)
	usort($x, "order_func")
	
	$arraylength = count($x);
	for ($a = 0; $a < $arraylength; $a++)
	{
	echo $x[$a];
	echo "<br>";
	}
	
	Output:
	2
	4
	6
	9
	12

Now with the introduction of  PHP 7s new spaceship operator, a order sorting function could look like this: 

    function order_func($x, $y) {
    return $x <=> $y;
    }
	
	$x = array(6,2,9,12,4)
	usort($x, "order_func")
	
	$arraylength = count($x);
	for ($a = 0; $a < $arraylength; $a++)
	{
	echo $x[$a];
	echo "<br>";
	}
	
	Output:
	2
	4
	6
	9
	12

See the difference in detail needed to create an ordering function? The addition of the spaceship operator makes the code easier to read, and understand. Before the spaceship operator, the developers at PHP have mentioned that it was common for programmers to incorrectly write ordering functions,  unsuccessfully try to debug it, and then submit a bug report to the PHP development team stating that usort( ) was not working correctly. 
Even though the spaceship operator can be used for other applications, one of the most appreciable applications of this will be for anyone looking to order a set of values. The spaceship operator isn't limited to integers and can also be used to compare: floats, strings, arrays, and even objects.  
Here is the syntax for the spaceship operator, and how it compares to the current operators:
(expression) <=> (expression)
	- If both operands are equal, it returns 0
	- If the left operand is greater than the right operand, it returns 1
	- If the right operand is greater than the left, it returns -1 

If that is a little hard to follow, here is a list of current comparison operators and their spaceship equivalent:
    
     operator      <==>  equivalent
    $x  <  $y         ($x <=> $y) === -1
    $x <= $y         ($x <=> $y) === -1 || ($x <=> $y) === 0
    $x == $y         ($x <=> $y) === 0
    $x ! = $y         ($x <=> $y) !== 0
    $x  >= $b         ($x <=>  $y)  ===  ($x  <=> $y) === 0
    $x > $y           ($x <=> $y) === 1 

Because they can be used to compare almost anything , the spaceship operator will be hugely helpful for any level programmer that is looking for a way to compare different types of code, and sort them accordingly. 

## The Null Coalesce Operator (??)
PHP developers are often tasked with setting up websites and servers to process user data. While this can be very complicated, there is a lot of boilerplate code that can be used as a template for a developer's specific purpose. However, often times, this still requires a lot of troubleshooting and debugging by the developer to make the boilerplate code fit their specific application's needs . PHP7 introduces the null coalesce operator as a solution to this problem. 

The easiest way to summarize the feature of this operator, is to consider the common programming task of checking if something has a value or not, and if no value exists, then automatically put in a default value in its place. 

Before PHP 7, you would typically have to write something like: 
    
    $user_options = isset($_GET['$user_options']) ? $_GET['$user_options'] : "$default_options"; 

This code requests the $user_options values from the server, and if the user doesn't have any selected options, it will load in the $default_options value instead. 

With the new Null Coalesce operator in PHP7, that code can be written as 
    $user_options = $_GET[user_options] ?? '$default_options';

The syntax is as follows: 
    (operand) ?? (operand)

This will return the result of the first operand, if: 

*    the value exists, and is not null. 
*    the value of the first operand doesn't exist, then it returns the second operand. 

In the example above, if the $user_options field hasn't been filled out, then program will return the default options. While this is a very simplified example, the reason this feature has been requested was because developers were running into problems with E_NOTICE being triggered if they left the default value as blank. 

### How will these new operators change future development using PHP?  

Both operators will be tremendously beneficial in reducing boiler plate code, and the amount of code necessary to perform detailed operations. This really does go to show you that PHP 7's development's team goal of "making the internet faster" was delivered to the PHP development community with the introduction of new "ease of life" features like the two new operators. 

Any level of programmer should begin immediately mastering these new operators, because proper understanding will result in adding more weapons to your problem solving toolbox. Another potential benefit of learning these operators at their introduction, is being able to effectively gauge the skill of any PHP developer. Since the operators have only just been introduced, these won't be included on many of the "learn to code" websites or language references for quite some time. Until these new operators become a standard part of any code on any template, being able to show properly demonstrate the application of these features will show your dedication to the PHP language.   
