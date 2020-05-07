lua把实际的char数组紧贴UTString结构来存储，所以一个string实际占用的大小是UTString结构大小加上char数组大小+1(结束符'\0')。

```
#define sizelstring(l)  (sizeof(union UTString) + ((l) + 1) * sizeof(char))
```
所以在从TString中获取实际字符串内容时，地址要在UTString地址之后

```
/*
** Get the actual string (array of bytes) from a 'TString'.
** (Access to 'extra' ensures that value is really a 'TString'.)
*/
#define getstr(ts)  \
  check_exp(sizeof((ts)->extra), cast(char *, (ts)) + sizeof(UTString))
```