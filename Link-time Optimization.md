https://groups.google.com/g/llvm-dev/c/DR0O3gTVBuA

Enabling LTO:
1. Register the pass so that it happen during LTO `EP_FullLinkTimeOptimizaitonLast` or `Early`
2. Enable `-flto`, load the pass in Clang, change linker to lld (not sure about gold linker). 
	1. e.g., `clang -flto -fuse-ld=lld -Wl,-mllvm=-load=pass.so`
