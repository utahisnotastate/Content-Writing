# PHP 7 Backwards Compatibility Guide 

PHP 7 was released in December 2015, and features substantial performance upgrades and features designed to make any website up to twice as fast. Below is a guide of major backwards compatibility issues you may face when upgrading your website from PHP 5.x to 7.0 

Please keep in mind, that upgrading your website to the newest version of any programming language without taking the appropriate steps of testing your code in a safe development environment is not advisable under many circumstances. Make sure you back up your website, and create a development environment where you can test the update before you deploy PHP7 to live servers. 

PHP 7's development team has reassured all users that there will be minimal disruption to any current code running in PHP 5, but there are three major points of focus that any developer should be aware of when upgrading to PHP 7. 

## Issue 1: Changes to  variable handling 
One of the major new features of PHP 7 is the implementation of an Abstract Syntax Tree. By including this feature in PHP 7, it adds features to PHP's parser that it lacked in previous versions of PHP. 
The introduction of the Abstract Syntax Tree requires that all PHP code written in version 7.0.x and onward must follow the same uniform variable syntax.
In previous versions of PHP when you indirectly accessed variables, properties, and methods they  were evaluated in case specific order. In PHP 7, and onward, these will now be ordered in a strictly left-to-right order. 
Old and new evaluation of indirect expressions

    Expression	  	           PHP 7 interpretation
    $$abc['bill']['net'] 	 ($$abc)['bill']['net'] 
    $abc->$bill['net'] 	 	($abc->$bill)['net'] 
    $abc->$bill['net']() 	($abc->$bill)['net']() 
    Abc::$bill['net']() 	(Abc::$bill)['net']() 

### Making PHP 5.x Code compatible with PHP 7

Code that used the old right-to-left evaluation order must be rewritten to explicitly use that evaluation order with curly braces .To fix the above example expressions in PHP 5.x to have the same PHP7 interpretation please consult the below table: 
			


    PHP 5.x Expression		                         Change to:				
    $$abc['bill']['net'] 	                    ${$abc)['bill']['net']} 
    $abc->$bill['net'] 	                        $abc->{$bill['net']} 
    $abc->$bill['net']() 	                    $abc->{$bill['net']}() 
    Abc::$bill['net']() 	                    Abc::{$bill['net']}() 

## Issue 2:  Changes in Variable and Integer Handling 

#### PHP will no longer automatically change invalid octal literals. 

An octal literal is a number that uses a base-8 number system.  Previously, octal literals that contained invalid numbers were automatically modified by PHP to be valid, but this functionality has been removed in PHP 7. For example, if your code produced the number  0168 in PHP 5.x, PHP would recognize that this was an invalid octal literal number, and would change the number to be 016 instead. If the same code is run in PHP7, it will give you a parse error. 

#### Changes to Dividing By Zero 

In PHP 5.X, If your code used either the divide (/) or modulus (%) operators to divide by zero, it would result in an E_WARNING and returned a false value.  

In PHP 7, this has been modify to have different results. If you divide by zero using the divide operator, it will return a float with one of the three following values: +INF, -INF, or NAN. 

If you use the modulus operator to divide by zero, the E_WARNING has been replaced with a "DivisionByZeroError" exception. 

#### Changes to list() 

In PHP 5.x list() would assign variables in reverse order. This has been changed in PHP 7 to assign values to variables in the exact order they are defined in instead. You will need to modify your code to not depend on the assignment order of list(). The development team has warned that variable assignment order could be changed again in a future update to PHP 7. Meaning, that variable assignment order could be changed back to reverse order like in PHP 5.x in a future patch to PHP 7. 

You will no longer be allowed to have empty list() assignments which was allowed in previous versions of PHP. 

Lastly,  you can no longer use list() to unpack strings. If you have code that uses list() for this purpose, the development team has recommended you use str_split() instead. 

## Issue 3: Deprecated/ Removed Features in PHP 7 

There aren't too many deprecated features in PHP7, and thankfully most users really should not run into problems with any of the features listed below. These features were mostly phased out in PHP 4, and were finally removed from PHP in this latest release. 

#### PHP 4.0.x constructors 

If you have not upgraded from PHP 4, and would like to move to PHP 7 be wary if you are still using PHP 4 constructors. If the methods in your constructor have the same exact name as the class they are defined in, this will cause an error in PHP 7.  When you test the code in PHP 7, the affected code will emit an E_DEPRECATED error. 

##### ASP and script PHP tags are no longer supported 
You are no longer allowed to use ASP and script tags to delimit PHP.  The affected tags are:
Opening Tag:                 Closing tag 
<%                            	%>
<%=                  	        %>
<script language="php">	</script>

##### List of new reserved words: 

Please make sure your PHP 5.x code is free from using any of the following names to name classes, interfaces or traits: "bool", "int", "float", "string", "NULL", "TRUE", and "FALSE". 
If you find yourself with code that uses any of the names above, you will need to change them to something else for your code to work in PHP 7.x. Additionally, please go through your PHP 5.X code and make sure that the following names aren't used either: "resource", "object", "mixed", and "numeric". These names aren't invalid in PHP 7, but PHP 7's development team has stated that those names will be used in forthcoming versions of PHP 7.x, so it is better to remove them now before they eventually become incompatible with future versions of PHP 7. 

###Tips for testing your code in PHP 7 ###

PHP 7's development team have provided users with a static analyzer, named PHAN, to help test your PHP code for compatibility with PHP 7. For example, If you are worried about your code not conforming to the Uniform Variable Syntax, one of PHAN's features is being able to check for correct uniform variable syntax. 
PHAN has the ability to analyze the code for any version of PHP, and is heavily recommended by PHP's development team that you setup PHAN to test your code. 
 Detailed setup instructions can be found on [github](https://github.com/etsy/phan)

