---
tags : cpp
---


## 靜態鏈接
編譯時，把所有函式一起包進exe內
   * 優點：
      * 引用簡單
      * 包裝簡單
   * 缺點：
      * 佔用內存
      * 不便於維護與擴展，lib更動，也需要更改exe
	
```bash
ar -crs libdllSpec.a BST_int.o dllSpec.o
```
## 動態鏈接
exe可以動態卸載與引用dll
   * 優點：
      * 當有多個exe同時用到一份dll時，不會重複載入
      * dll與exe獨立，接口不換，更換dll不會對exe造成影響
   * 缺點：
      * link時較慢，load更慢

Link方式：
* Load-time Dynamic Linking：
編譯前已經明確知道要調用那些函數，保留必要鏈接訊息
需要一起加入編譯

* Run-time Dynamic Linking：
```c
//testdll.h
#ifdef DLL_EXPORT
    #define DLLAPI __declspec(dllexport)
#else
    #define DLLAPI __declspec(dllimport)
#endif


DLLAPI float funadd(float a, float b);

```
```shell
gcc -c -DDLL_EXPORT -fPIC testdll.c
gcc -shared -o testdll.dll testdll.o -Wl,--output-def,testdll.def,--out-implib,testdll.lib
gcc -c testmain.c
gcc -static -o test.exe testmain.o -L. -ltestdll
```
`-Wl`將參數傳給連接器
`-DDLL_EXPORT`編譯時define DLL_EXPORT
