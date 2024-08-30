First Lecture 
<mark style="background: #ADCCFFA6;">Text like this notes taken that are not on slides , CMD+H</mark>
<mark style="background: #FFF3A3A6;">Text like this are for important points from either the slides or the textbook </mark>

<mark style="background: #ADCCFFA6;">STL Documentation</mark>
- https://cplusplus.com/reference/
- https://www.cppreference.com/Cpp_STL_ReferenceManual.pdf

<mark style="background: #ADCCFFA6;">Unordered maps are implementing using hashmaps that have very effieicent insert and delete command</mark> 

<mark style="background: #ADCCFFA6;">If you delete a cell from the middle of a vector, something NEEDS to be done because a gap can't exist in a vector.</mark>
- <mark style="background: #ADCCFFA6;">shift every value over to fill in the gap</mark> 
- <mark style="background: #ADCCFFA6;">rewrite the vector to a new vector without the gap</mark>
*vector.erase() deletes a cell and shifts everything into place*

<mark style="background: #ADCCFFA6;">To avoid this problem altogether we could just use a linked list so we only need to reorganize a few pointers, but then we would have to think about traversal.</mark>
*List.erase() will delete a cell and then fix the pointer of the preceeding cell*

<mark style="background: #ADCCFFA6;">Each data structure has it own internal structure so each of there functions are implemented differently and so will have different efficiencies. Every data structure has strengths and weaknesses that we need to think about, in order to have the most efficient solution. </mark>

<mark style="background: #ADCCFFA6;">A map can be made using trees, hashmaps and arrays. But the chosen container decided the effiecieny and utility of every function used by that map.</mark> 


#### Move Semantics (Slide 1)
- Semantics describes the processes a computer follows when
executing a program in a specific language.
- Move semantics in C++ were greatly improved in C++11 by the introduction of rvalue references, move constructors, and move assignment operators. This made it easier to transfer allocated memory to another object when needed, rather than copying and deleting.

- #### Let's review the basics covered in the textbook.
	- What is an rvalue?
	- What is the syntax for rvalue references?
	- How is function overloading used to enable move semantics?
	- Let's look at 1.5.2 and 1.5.6 for the answers.

<mark style="background: #ADCCFFA6;">Reasignin values and then moving the mis usually more efficent than copying to another variable and deleteing the orginal. This is the crux of move semantics, when can we use this mindset to make our code more efficient</mark>

We will use them in two ways, when making
- constructors
- assignment operators


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
