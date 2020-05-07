union的数据长度
1.大小大于等于最大成员
2.大小是其所包含的基本数据类型的整数倍

```
union   MyUnion {
	char   a;   
	int   b[5];     
	int   d[3];
};

int main() {
	MyUnion u;
	std::cout << "size : " << sizeof(u) << "\n";
	getchar();
}
//输出 size : 20 由于int是4字节，b数组暂用20字节；
```

```
union   MyUnion {
	char   a;   
	int   b[5];
	double c;     
	int   d[3];
};
//输出 size : 24 由于其包含的基本数据类型double是8字节，其大小必须是8的整数倍。
```

#关于union强制类型转换
此例子中将int转为char,其原理是union数据公用内存。
```
union DoubleToChar{
	int d;
	char c[8];
}dtc;

int main() {
	dtc.d = 255;
	std::cout << dtc.c;
	getchar();
}
```
![union转换结果](/pic/union_int2char.PNG)