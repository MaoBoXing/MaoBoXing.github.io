# 前言

`winafl` 是 `afl` 在 `windows` 的移植版， `winafl` 使用 `dynamorio` 来统计代码覆盖率，并且使用共享内存的方式让 `fuzzer` 知道每个测试样本的覆盖率信息。本文主要介绍 `winafl` 不同于 `afl` 的部分，对于 afl 的变异策略等部分没有介绍，对于 `afl` 的分析可以看

```avrasm
https://paper.seebug.org/496/#arithmetic
```

# 源码分析