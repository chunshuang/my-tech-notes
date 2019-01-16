# Problem

Source: http://yeasy.blogspot.com/2011/11/blog-post.html

# My Algorithm

In C

```c
#include <stdio.h>

const int threshold = 30; // floor from which the egg will be broken
int count = 0;

int test(int floor) {
	printf("Try floor %d\n", floor);
	count++;
	return floor >= threshold ? 0 : 1;
}

int find(int min, int max) {
	int middle = (max+min) / 2;

	if (test(middle) == 0) { // eggA was broken
		int i = 0;
		for (i = min; i <= middle; i++) {
			if (test(i) == 0) // find it
				break;
		}
		return i;
	} else { // eggA survived
		return find(middle, max); // recursive call
	}
}

int main() {
	int r = find(1, 100);
	printf("The floor is: %d, tried %d times.", r, count);
	// The following line has different behavior between LLVM (Darwin) and gcc (Linux/bsd).
	// Think why?
	// printf("The floor is: %d, tried %d times.", find(1, 100), count);
	return 0;
}
```

# My thinking

The 'count' depends on the real answer, e.g.:

- for threshold = 30, the count is 31
- for threshold = 90, the count is 8

The more close to the upper boarder of the scope, the fewer test needed.

I don't get the conclusion of source (http://yeasy.blogspot.com/2011/11/blog-post.html).

**Is there any misunderstanding or blind-spot in my mind?**

# Misc

In the source code line 32, I found an instresting thing about compiler in different platforms.
