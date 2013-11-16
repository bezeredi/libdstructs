libdstructs
===========
Simple ANSI C Data Structures Library. This is generic data structures library
written in ANSI C. As of this moment, these implementations are not intended to
be C++ compatible or thread-safe.

This library will be as commented and self documenting as possible. I recognize
that many students who want to learn data structures have trouble with the
implementation aspect of data structures. This library will be an excellent
resource on how to build select data structures, with ANSI C anyway.

I found myself writing the same data structures over and over again in my
projects for school like linkedlists, queues, stacks, and hashtables. Many
times, this was born out of the restriction of not being able to use arrays in
projects. So, why not build a collection of the data structures most commonly
used and put them in a library for future use? There are a bunch of libraries
like this one out there. This library, `libdstructs`, was built to model the
basic functionality of the
[Java Collections Framework](http://docs.oracle.com/javase/7/docs/technotes/guides/collections/).

The list of data structures that will be included will be those that are fairly
commonplace, including, but not limited to, linkedlists, queues, vectors,
trees, sets, and hashtables.


Implemenation
-------------
`libdstructs` data structures are designed in such a manner so as to force the
idea of data encapsulation. This, unfortunately, means that memory allocation
is a must. Also to keep the user from unintentionally playing with pointers
which could mess up the underlying representation of the structure, data types
are implemented in an opaque manner. This means that the data types cannot be
allocated on the stack. Pointers must be used instead and must be accessed
though function calls explicitly. For example:

	void example(void){
		llist_t *list;	/* Pointer on stack */

		list = ll_init(int);	/* Allocation on the heap */

		.
		.
		.

		ll_free(list);
	}

is how you would create and destroy a linkedlist whose elements are of type
int. The following is an example of something that cannot be done:

	void example(void){
		llist_t list;	/* Allocation on the stack */

		.
		.
		.
	}

The compiler cannot determine how much space on the stack to make for the
linkedlist since the data type is opaque. All of that information is hidden
inside of the appropriate translation unit. Another example of something that
cannot be done is dereferencing pointers of these opaque data types:

	void example(void){
		llist_t *list;
		int number;

		list = ll_init(int);	/* Allocation on the heap */

		.
		.
		.

		number = list->size;	/* Error: dereferencing incomplete type */
	}

The compiler cannot calculate the offset into a structure that is incomplete.
As a result, the user will often see the error: dereferencing incomplete type.


Installation
------------
Coming soon.


Notes
-----
Graphs are not currently planned to be a part of this library. See
[libgstructs](https://github.com/bezeredi/libgstructs) for graph structure
implementations.


License
-------
The `libdstructs` library is distributed under the GNU General Public License
(GPL) version 3. See
[LICENSE](https://github.com/bezeredi/libdstructs/blob/master/LICENSE) for more
information.

