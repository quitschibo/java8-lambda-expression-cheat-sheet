java8-lambda-expression-cheat-sheet
===================================
General
-------
`a -> a + 1;` // take `a` as parameter and return `a + 1`

`(b, c) -> b + c;` // take `(b, c)` as parameter and return b + c

`LambdaInterface myLambda = (c, d, e, f) -> c + d + e + f;` // take `(c, d, e, f)` as parameter and return the sum as return value. The lambda implements `LambdaInterface` and has the name `myLambda`.

Example
-------
<pre>    
  /**
   * The interface of my lambda
   */
  interface LambdaInterface {
	  String doSomething(String message);
  }
  
  /**
   * This is the method which should use my lambda expression
   */
  public static void lamdaUsingMethod(String messageToLog, LambdaInterface lambda) {
	  System.out.print(lambda.doSomething(messageToLog));
  }
  
  /**
   * The main method which run the testprogram
   */
  public static void main(String[] args) {
	  // here we build the lambda expression
	  LambdaInterface errorMessage = (message) -> "Error: " + message;
    
    // here we use the lambda to so something
	  lamdaUsingMethod("This is my testmessage", errorMessage);
  }
</pre>
