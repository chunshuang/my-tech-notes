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

# Update (Jan 17th)

After re-read the source again in the morning, I suddenly understand the meaning of this problem:

**How to determine which floor to start?**

My blind-spot is that I set the N to 50 predictably since I use the classic two-divide method.

But is the 'middle' of (1, 100) is a good choice? No, the answer comes from probability.
Because we don't know the k (the threshold in C program above). And we have to find a good way to guess without knowing the k in advance.

Here is the point: **my puzzel is that I always think with known k and never think when k is unknown**

I use "if k blabla ... else ..." as the answer, and never give the real answer. The real answer is the actual value of N to start. Not the logic judegment. It's a decision, an action.
