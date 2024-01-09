# BypassAv
将干净的ntdll.dll替换被杀软监控的ntdll.dll

# 实现步骤
1.获取 ntdll.dll的模块句柄和信息，包括它在内存中的基地址。

2.以只读方式打开 c:\\windows\\system32\\ntdll.dll文件，并创建一个文件映射。然后，将这个文件映射到内存中。

3.获取 ntdll.dll在内存中的 DOS 和 NT 头部信息。

4.遍历 ntdll.dll的所有节（section）。如果发现了名为 .text的节，这个节通常包含了 DLL 的代码，那么就需要解除对它的钩子。

5.使用 VirtualProtect函数修改 .text节的内存保护属性，使其可以读写执行。

6.使用 memcpy函数将原始的 ntdll.dll文件中的 .text节复制到内存中的 ntdll.dll的对应位置，从而覆盖可能被修改的代码。

7.再次使用 VirtualProtect函数恢复 .text节的内存保护属性。

8.关闭文件句柄和文件映射，释放模块。
