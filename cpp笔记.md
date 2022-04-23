## 相同class的各个object互为friends
2，temp object 临时对象 typename();
eg:
```
Complex func(doble x, double y){
    return Complex (real(x),imag());
}
```
##  new具体做了什么
new:先分配memory，再掉用constructor

eg:
```
Complex* pc = new Complex(1,2);
//Complex::Complex(this,1,2);
```
编译器转化为：
```
void* mem = operator new( sizeof(Complex) );//分配内存
pc = static_cast<Complex*>(men);//转型
pc->Complex::Complex(1,2);//构造函数
```

## delete具体做了什么
delete: 先调用destructory,再释放memory
```
String* ps = new String("Hello");
...
delete ps;
```
编译器转化为：
```
String::~String(ps);//析构函数（释放对象动态创建的内存）
operator delete(ps);//释放内存（释放指针占用的内存）
//delete内部掉用free(ps)
```
## array new一定要搭配array delete使用
```
String* p = new String[3];
...
delete[] p; //唤起3次destructory
```

```
String* p = new String[3];
...
delete p; //唤起1次destructory;
```

## 拷贝复制要注意的写法
inline
```
String& String::operator=(const String& str)
{
    if(this == &str){
        return *this;
    }
    delete[] m_data;
    m_data = new char[strlen(str.m_data) + 1];
    strcpy(m_data, str.m_data);
    return *this;
}
```