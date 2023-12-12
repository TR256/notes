今天调试代码时发现出现```int index = false```这样代码，很是诧异

编译器会在编译的时候对代码进行优化，没有被使用的int变量值会被优化为true或者false（不等于0为true，等于零为false），反编译时不能够反编译回原来的int型数值，于是就留下了 ```int index = false```这样的代码
