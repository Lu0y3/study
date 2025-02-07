1. 为什么类构造函数中调用虚函数是静态绑定？(C++中，C#可以调用虚函数动态)
   答：**子类构造函数先调用父类构造函数。类构造函数执行后才能执行类的其他方法。更底层的解释是：基类的构造函数会将虚函数表指针指向基类的虚函数表，因此调用虚函数的时候实际上是调用基类的虚函数。** 如RedHouse()构造函数会先调用House()构造函数，后者执行虚函数方法this->buildfunc1()，假设是动态绑定，那么在子类构造函数RedHouse()还未执行完之前(此时父类构造函数House()还未结束)，就调用子类的virtual override方法，是矛盾的，所以不是动态绑定。
``` C++
情景：
class House{
public:
    House(){
        this->buildfunc1(); //静态绑定 执行的是House的方法
    }
protected:
    virtual void buildfunc1() = 0;
}

class RedHouse : public House{
public:
    RedHouse(){

    }
protected:
    virtual void buildfunc1() override;
}
```

