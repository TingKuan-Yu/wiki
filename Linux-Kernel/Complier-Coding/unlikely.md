# https://stackoverflow.com/questions/109710/how-do-the-likely-unlikely-macros-in-the-linux-kernel-work-and-what-is-their-ben
- example: avoid runing dosomething()
```
These are macros that give hints to the compiler about which way a branch may go. The macros expand to GCC specific extensions, if they're available.

GCC uses these to to optimize for branch prediction. For example, if you have something like the following

if (unlikely(x)) {
  dosomething();
}

return x;
Then it can restructure this code to be something more like:

if (!x) {
  return x;
}

dosomething();
return x;
The benefit of this is that when the processor takes a branch the first time, there is significant overhead, because it may have been speculatively loading and executing code further ahead. When it determines it will take the branch, then it has to invalidate that, and start at the branch target.

Most modern processors now have some sort of branch prediction, but that only assists when you've been through the branch before, and the branch is still in the branch prediction cache.

There are a number of other strategies that the compiler and processor can use in these scenarios. You can find more details on how branch predictors work at Wikipedia: http://en.wikipedia.org/wiki/Branch_predictor



```