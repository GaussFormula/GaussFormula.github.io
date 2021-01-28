# 如何对一个shared_ptr数组使用qsort？
Preface：这是在抄Ray Tracing The Next Week的时候遇到的问题。BVH那一章的排序，作者用的是二级指针，我觉得挺难看，于是打算用STL容器改写一下，在改写的过程中碰到了该情况。

```
class Data
{
public:
        Data(int _i)
        :i(_i)
        {}
        
        int i;
}
```

```
int main()
{
    std::vector<std::shared_ptr<Data>> v;
    v.push_back(std::make_shared<Data>(3));
    v.push_back(std::make_shared<Data>(2));
    v.push_back(std::make_shared<Data>(1));

    std::qsort(&v[0],v.size(),sizeof(std::shared_ptr<Data>),
    [](const void* a,const void* b)->int
    {
        std::shared_ptr<Data> temp_a=*((std::shared_ptr<Data>*)a);
        std::shared_ptr<Data> temp_b=*((std::shared_ptr<Data>*)b);

        if(temp_a->i<temp_b->i)
        {
            return -1;
        }
        else
        {
            return 1;
        }
    });

    return 0;
}
```

作为一个记录。