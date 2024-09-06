#### Move Constructor Example
- Consider the Foo class with these members:
	– int num1;
	– char* word1; // pointer to dynamically allocated character array
	– std::string word2;
- Then the move constructor would be written like this:
```
Foo::Foo(Foo&& rhs) {
	num1 = rhs.num1;
	word1 = rhs.word1;
	rhs.word1 = nullptr;
	word2 = std::move(rhs.word2); // move constructor usually cleans up
	}
```
- If the source (rhs) is a temporary object, it can safely expire.
- If the source is an lvalue that has been cast to an rvalue using std::move, the object will still be there, but it will be in a non-specified state (and safe to delete).
*Never use a variable after using a move function on it*

#### Move Assignment Operator Example 
- And the move assignment operator would be this: 
```
Foo& Foo::operator=(Foo&& rhs) { 
	if (this != &rhs){ 
	num1 = rhs.num1;
	delete[] word1;
	word1 = rhs.word1;
	rhs.word1 = nullptr;
	word2 = std::move(rhs.word2);
	}
return *this; 
} 
```
##### What do we do here that we didn't do for the constructor, and why?
- <mark style="background: #ADCCFFA6;">delete[] word1;</mark> // we need to delete the original word1 after moving it
- <mark style="background: #ADCCFFA6;">if(this !=&rhs)</mark> // the move assignment needs to make sure that the both the starting and end point for the move assignment are different (because we end up deleting the word in it entierty)
- <mark style="background: #ADCCFFA6;">return *this</mark> // return a pointer the newly assigned object 

### Chapter 2
Big O [Upper Bound]= the worst case scenario of time needed to run the number of actions in a program (worst case scenario in terms of run-time) 

![[Pasted image 20240906115652.png]]

#### Maximum Subsequence Problem
![[Pasted image 20240906124603.png]]
