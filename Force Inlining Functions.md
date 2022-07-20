The problem: I'm trying to instrument the program's load and store instruction with wrapper that modify the pointer in the value. Since there are a lot of load/store, and the wrapper is short, I expect inlining would leads to better performance.

I tried to force inline with the function attribute `__attribute__((__always_inline__))` but it did not work. LLVM would not listen.

Luckily `Lib/Transform/Utils/Cloning.h` provide a function call `InlineFunction(CallInst, ...)` when invoked it would try to inline the call instruction. 

Hence I used two step to inline every calls. The first step instrument the function call normally, but store the inserted LLVM's CallInst in an array. After instrumentation is done, I loop through the array to invoke `InlineFunction` on them.



