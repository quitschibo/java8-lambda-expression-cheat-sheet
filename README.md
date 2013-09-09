java8-lambda-expression-cheat-sheet
===================================
General
-------
`a -> a + 1;` // take `a` as parameter and return `a + 1`

`(b, c) -> b + c;` // take `(b, c)` as parameter and return b + c

`LambdaInterface myLambda = (c, d, e, f) -> c + d + e + f;` // take `(c, d, e, f)` as parameter and return the sum as return value. The lambda implements `LambdaInterface` and has the name `myLambda`.

Collections
-----------
Iterate a list:
`list.forEach(i -> System.out.print("Element: " + i);`

Iterate a list with filtering:
<pre>
list.stream()
	.filter(i -> i % 3 == 0) 
	.forEach(i -> System.out.print("Element: " + i));
</pre>

Filtering and mapping:
<pre>
list.stream()
	.filter(i -> i % 3 == 0)
	.map(i -> new Double(i))
</pre>

Filtering, mapping and collecting:
<pre>
ArrayList<Double> doubleList = list.stream()
	.filter(i -> i % 3 == 0)
	.map(i -> new Double(i))
	.collect(Collectors.toCollection(ArrayList::new));
</pre>

Parallel vs Sequential
----------------------
You can run the mapping and filtering sequential:
<pre>
// if the ints are ordered in list, the result will be ordered, too
list.stream()
	.sequential()
	.filter(i -> i % 3 == 0)
	.map(i -> new Double(i))
	.forEach(i -> System.out.println("Element: " + i));
</pre>
You can run it parallel:
<pre>
// even if the ints are ordered in list, the result will NOT be ordered
list.stream()
	.parallel()
	.filter(i -> i % 3 == 0)
	.map(i -> new Double(i))
	.forEach(i -> System.out.println("Element: " + i));
</pre>
BUT:
<pre>
// if the list is ordered, the result will be ordered too, even if it is processed parallel.
// rule of thumb: if you expect it to be ordered, it will be ordered (lists, arrays, etc.)
ArrayList<Double> result = list.stream()
	.parallel()
	.filter(i -> i % 3 == 0)
	.map(i -> new Double(i))
	.collect(Collectors.toCollection(ArrayList::new));
</pre>

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
