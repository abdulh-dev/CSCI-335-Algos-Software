Second Lecture
<mark style="background: #ADCCFFA6;">Text like this notes taken that are not on slides , CMD+H</mark>
<mark style="background: #FFF3A3A6;">Text like this are for important points from either the slides or the textbook </mark>

#### What is an rvalue?
An <mark style="background: #FFF3A3A6;">lvalue</mark> is an expression that identifies a non-temporary object. 

An<mark style="background: #FFF3A3A6;"> rvalue</mark> is an expression that identifies a temporary object or is a value (such as a literal constant) not associated with any object.

As examples, consider the following:

    vector<string> arr( 3 );
    const int x = 2;
    int y;

      ...
    int z = x + y;
    string str = "foo";
    vector<string> *ptr = &arr;

With these declarations, arr, str, arr[x], &x, y, z, ptr, *ptr, (*ptr)[x] are all lvalues. Additionally, x is also an lvalue, although it is not a modifiable lvalue.

For the above declarations 2, "foo", x+y, str.substr(0,1) are all rvalues. 2 and "foo" are rvalues because they are literals.


In C++11, a<mark style="background: #FFF3A3A6;">n lvalue reference</mark> is declared by placing an & after some type. An lvalue reference then becomes a synonym (i.e., another name) for the object it references. For instance,

	string str = "hell";
	string & rstr = str;
	rstr += ’o’;
	bool cond = (&str == &rstr);
	string & bad1 = "hello";
	string & bad2 = str + "";
	string & sub = str.substr( 0, 4 ); // illegal: str.substr( 0, 4 ) is not an lvalue

Lvalue reference uses:
- lvalue references use #1: aliasing complicated names
- lvalue references use #2: range for loops
- lvalue references use #3: avoiding a copy
- 

In C++11, <mark style="background: #ADCCFFA6;">an rvalue</mark> reference is declared by placing an && after some type. An rvalue reference has the same characteristics as an lvalue reference except that, unlike an lvalue reference, an rvalue reference can also reference an rvalue (i.e., a temporary). For instance,

    string str = "hell";
    string && bad1 = "hello";           // Legal
    string && bad2 = str + "";          // Legal
    string && sub = str.substr( 0, 4 ); // Legal



For IntCell, the signatures of these operations are

	~IntCell( );// Destructor
	IntCell( const IntCell & rhs );// Copy constructor
	IntCell( IntCell && rhs );// Move constructor
	IntCell & operator= ( const IntCell & rhs );// Copy assignment
	IntCell & operator= ( IntCell && rhs );// Move assignment



<mark style="background: #ADCCFFA6;">If an integer was a data member of an object that objects move constructor would copy the integer</mark>

<mark style="background: #ADCCFFA6;">you don't move static memory, only dynamically allocated memory </mark>




#### Original Motivation Slide 2/8 
- Here's an explanation of the original motivation for adding rvalue references in C++ 11: https://www.open-std.org/jtc1/sc22/wg21/docs/papers/2006/n2027.html
- Note how pointer and class data members are handled. This doesn't show primitive data types, because they don't use or need move semantics (nor should they... why not?)
- The parts of objects that are moved rather than copied are sometimes called “external resources” and are typically dynamically allocated. In normal use, they'd always or almost always be dynamically allocated.

#### Writing a Move Constructor Slide 3/8
- When writing a move constructor, these types of data members are dealt with as such: 
	- <mark style="background: #FFF3A3A6;">Primitive data types are just copied. </mark>
	- <mark style="background: #FFF3A3A6;">Pointers to dynamically allocated memory (i.e. resources in the heap) are copied then deleted from the source, effectively transferring ownership of the resource it points to.</mark> 
	- <mark style="background: #FFF3A3A6;">(Nested) objects are turned to rvalues using std::move, thus invoking their own move constructors (in a recursive-like manner). </mark>
	- For pointers to static memory (i.e. resources on the stack), it becomes a bit more complicated, since you need to consider the scope and lifetime of the resource. However, the need to do this rarely arises, and we're unlikely to encounter it in our projects.

#### std::move Slide 4/8
- Let's take a look at the C++ documentation for std::move https://en.cppreference.com/w/cpp/utility/move 
- All std::move actually does is to convert to an rvalue. 
- But passing an rvalue to a function that uses move semantics has certain implications, such as: 
	- An object with a move constructor will use that rather than its copy constructor. 
	- Other functions may be overloaded to move when passed an rvalue, but copy when passed an lvalue. 
	- When a resource is moved, the source must be left in a “valid but unspecified state” that is safe to delete. 
- Let's also take a look at std::swap. When should each be used, and why? https://en.cppreference.com/w/cpp/algorithm/swap

<mark style="background: #ADCCFFA6;">if you use std::move on an lvalue, it turns it into an rvalue</mark>
<mark style="background: #ADCCFFA6;">it doesn't delete the lvalue but returns an rvaliue reference for th lvalue </mark>

How you've been using move semantics 
- If you've ever done something like this in C++11 or higher, you've used move semantics: 

	```
	std::string foo() 
	{
	 std::string a = “hello world”; 
	 return a; 
	} 
	std::string b = foo(); 
	```

*Focus on overloading Rvalues and Lvalues
Focus on use cases for both Rand Lvalues



What would happen here before C++11, and what would happen in C++11 and higher? 
- As of C++11, foo() returns an rvalue reference, which invokes the string class's move constructor. Prior to C++11, the string returned from foo() would be copied to b, which is inefficient. 
- One more question: as previously stated, moving an object must leave the source in a state that is safe to delete. Why does that matter in this case?


#### What's up next?
Algorithmic analysis
Big O notation
- little O
- theta
Chapter 2 

