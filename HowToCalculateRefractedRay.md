# 折射光向量的推导过程
Preface: 推导的起因是在阅读并实现`[Ray tracing in one weekend]`中的代码时遇到了一段不明所以的代码。

代码如下：
```
bool refract(const vec3& v,const vec3& n,float ni_over_nt,vec3& refracted)
{
    vec3 uv=unit_vector(v);
    float dt=dot(uv,n);
    float discriminant=1.0f-ni_over_nt*ni_over_nt*(1.0f-dt*dt);
    if(discriminant > 0)
    {
        refracted=ni_over_nt*(v-n*dt)-n*sqrt(discriminant);
        return true;
    }
    else
    {
        return false;
    }
}
```
通过查阅资料得知，这段代码是在计算折射光向量，但由于作者略去了推导过程，便很难理解其中用意。

本文以下的推导过程，是受到一篇博文的启发而完成的，在此致谢。
[折射向量计算](https://www.cnblogs.com/theWhisper/p/10269574.html)

## 推导过程:

![折射光线传播路径示意图](http://ezphysics.nchu.edu.tw/physiweb/down/html/dispersion.files/image008.jpg)

**n1**与**n2**分别是入射光与折射光所在介质的折射率。

设入射光为***I***，折射光为***T***，法线为***N***，垂直于平面向上，切向量***G***垂直于法线***N***，处于两种介质交界处，且方向向右。

以上所有向量均为单位向量。

显然，由于法线***N***与切线***T***互相垂直，且都是单位向量，他们组成了一组正交基，可以构成一组坐标系。所以可以将向量***T***分解为a\****N***+b\****G***

>***T*** = a\****N*** + b\****G***

a\****N***是向量***T***在***N***方向的投影，所以有

<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{120}&space;\large&space;\left&space;(\vec{T}*\vec{N}&space;\right&space;)*\vec{N}=a*\vec{N}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{120}&space;\large&space;\left&space;(\vec{T}*\vec{N}&space;\right&space;)*\vec{N}=a*\vec{N}" title="\large \left (\vec{T}*\vec{N} \right )*\vec{N}=a*\vec{N}" /></a>

又因为

<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{120}&space;\large&space;\vec{T}*\vec{N}=cos\left&space;(&space;\pi&space;-\theta&space;_{2}&space;\right&space;)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{120}&space;\large&space;\vec{T}*\vec{N}=cos\left&space;(&space;\pi&space;-\theta&space;_{2}&space;\right&space;)" title="\large \vec{T}*\vec{N}=cos\left ( \pi -\theta _{2} \right )" /></a>

联立可得

<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{120}&space;\large&space;a=-cos\theta&space;_{2}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{120}&space;\large&space;a=-cos\theta&space;_{2}" title="\large a=-cos\theta _{2}" /></a>

b\****G***是向量***T***在G方向上的投影，所以有

<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{120}&space;\large&space;\left&space;(&space;\vec{T}*\vec{G}&space;\right&space;)*\vec{G}=b*\vec{G}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{120}&space;\large&space;\left&space;(&space;\vec{T}*\vec{G}&space;\right&space;)*\vec{G}=b*\vec{G}" title="\large \left ( \vec{T}*\vec{G} \right )*\vec{G}=b*\vec{G}" /></a>

又因为

<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{120}&space;\large&space;\vec{T}*\vec{G}=cos\left&space;(&space;\frac{\pi}{2}-&space;\theta&space;_{2}&space;\right&space;)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{120}&space;\large&space;\vec{T}*\vec{G}=cos\left&space;(&space;\frac{\pi}{2}-&space;\theta&space;_{2}&space;\right&space;)" title="\large \vec{T}*\vec{G}=cos\left ( \frac{\pi}{2}- \theta _{2} \right )" /></a>

联立可得

<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{120}&space;\large&space;b=sin\theta_{2}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{120}&space;\large&space;b=sin\theta_{2}" title="\large b=sin\theta_{2}" /></a>

但问题来了，切向量***G***尚未求出，我们应该如何得到切向量***G***呢？

<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{120}&space;\large&space;\vec{I}*\vec{G}=cos\left&space;(&space;\frac{\pi}{2}-\theta&space;_{1}&space;\right&space;)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{120}&space;\large&space;\vec{I}*\vec{G}=cos\left&space;(&space;\frac{\pi}{2}-\theta&space;_{1}&space;\right&space;)" title="\large \vec{I}*\vec{G}=cos\left ( \frac{\pi}{2}-\theta _{1} \right )" /></a>

入射光向量***I***在切线方向***G***上的投影长度为<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{120}&space;\large&space;sin\theta&space;_{1}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{120}&space;\large&space;sin\theta&space;_{1}" title="\large sin\theta _{1}" /></a>

入射光向量***I***在切线方向***G***上的分量可用向量四则运算表示为

<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{120}&space;\large&space;\vec{I}&plus;\left&space;(&space;-\vec{I}*\vec{N}&space;\right&space;)*\vec{N}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{120}&space;\large&space;\vec{I}&plus;\left&space;(&space;-\vec{I}*\vec{N}&space;\right&space;)*\vec{N}" title="\large \vec{I}+\left ( -\vec{I}*\vec{N} \right )*\vec{N}" /></a>

归一化变为单位向量

<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{120}&space;\large&space;\frac{\vec{I}&plus;\left&space;(&space;-\vec{I}*\vec{N}&space;\right&space;)*\vec{N}}{sin\theta&space;_{1}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{120}&space;\large&space;\frac{\vec{I}&plus;\left&space;(&space;-\vec{I}*\vec{N}&space;\right&space;)*\vec{N}}{sin\theta&space;_{1}}" title="\large \frac{\vec{I}+\left ( -\vec{I}*\vec{N} \right )*\vec{N}}{sin\theta _{1}}" /></a>

所以切线向量***G***就推导出来了:

<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{120}&space;\large&space;\vec{G}=\frac{\vec{I}&plus;\left&space;(&space;-\vec{I}*\vec{N}&space;\right&space;)*\vec{N}}{sin\theta&space;_{1}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{120}&space;\large&space;\vec{G}=\frac{\vec{I}&plus;\left&space;(&space;-\vec{I}*\vec{N}&space;\right&space;)*\vec{N}}{sin\theta&space;_{1}}" title="\large \vec{G}=\frac{\vec{I}+\left ( -\vec{I}*\vec{N} \right )*\vec{N}}{sin\theta _{1}}" /></a>

综上，由***T*** = a\****N*** + b\****G***可推导出:

<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{120}&space;\large&space;\vec{T}=-cos\theta&space;_{2}*\vec{N}&plus;sin\theta&space;_{2}*\frac{\vec{I}&plus;\left&space;(&space;-\vec{I}*\vec{N}&space;\right&space;)*\vec{N}}{sin\theta&space;_{1}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{120}&space;\large&space;\vec{T}=-cos\theta&space;_{2}*\vec{N}&plus;sin\theta&space;_{2}*\frac{\vec{I}&plus;\left&space;(&space;-\vec{I}*\vec{N}&space;\right&space;)*\vec{N}}{sin\theta&space;_{1}}" title="\large \vec{T}=-cos\theta _{2}*\vec{N}+sin\theta _{2}*\frac{\vec{I}+\left ( -\vec{I}*\vec{N} \right )*\vec{N}}{sin\theta _{1}}" /></a>

由于折射发生时会遵循[Snell's law](https://en.wikipedia.org/wiki/Snell%27s_law)，入射角与折射角有如下关系：

![Snell's law](https://wikimedia.org/api/rest_v1/media/math/render/svg/b5a73124df21668801a4d20054bb1b13f6709752)

所以前项式可化为：

<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{120}&space;\large&space;\vec{T}=-cos\theta&space;_{2}*\vec{N}&plus;\frac{n_{1}}{n_{2}}*\left&space;[&space;\vec{I}&plus;\left&space;(&space;-\vec{I}*\vec{N}&space;\right&space;)*\vec{N}&space;\right&space;]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{120}&space;\large&space;\vec{T}=-cos\theta&space;_{2}*\vec{N}&plus;\frac{n_{1}}{n_{2}}*\left&space;[&space;\vec{I}&plus;\left&space;(&space;-\vec{I}*\vec{N}&space;\right&space;)*\vec{N}&space;\right&space;]" title="\large \vec{T}=-cos\theta _{2}*\vec{N}+\frac{n_{1}}{n_{2}}*\left [ \vec{I}+\left ( -\vec{I}*\vec{N} \right )*\vec{N} \right ]" /></a>


<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{120}&space;\large&space;\vec{T}=-\sqrt{1-sin^{2}\theta&space;_{2}}*\vec{N}&plus;\frac{n_{1}}{n_{2}}*\left&space;[&space;\vec{I}&plus;\left&space;(&space;-\vec{I}*\vec{N}&space;\right&space;)*\vec{N}&space;\right&space;]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{120}&space;\large&space;\vec{T}=-\sqrt{1-sin^{2}\theta&space;_{2}}*\vec{N}&plus;\frac{n_{1}}{n_{2}}*\left&space;[&space;\vec{I}&plus;\left&space;(&space;-\vec{I}*\vec{N}&space;\right&space;)*\vec{N}&space;\right&space;]" title="\large \vec{T}=-\sqrt{1-sin^{2}\theta _{2}}*\vec{N}+\frac{n_{1}}{n_{2}}*\left [ \vec{I}+\left ( -\vec{I}*\vec{N} \right )*\vec{N} \right ]" /></a>

由于

<a href="https://www.codecogs.com/eqnedit.php?latex=sin^{2}\theta&space;_{2}=\frac{n_{1}^{2}}{n_{2}^{2}}\cdot&space;sin^{2}\theta_{1}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?sin^{2}\theta&space;_{2}=\frac{n_{1}^{2}}{n_{2}^{2}}\cdot&space;sin^{2}\theta_{1}" title="sin^{2}\theta _{2}=\frac{n_{1}^{2}}{n_{2}^{2}}\cdot sin^{2}\theta_{1}" /></a>

<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{120}&space;\large&space;\vec{T}=-\vec{N}\sqrt{1-\frac{n_{1}^{2}}{n_{2}^{2}}*sin^{2}\theta&space;_{1}}&plus;\frac{n_{1}}{n_{2}}*\left&space;[&space;\vec{I}&plus;\left&space;(&space;-\vec{I}*\vec{N}&space;\right&space;)*\vec{N}&space;\right&space;]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{120}&space;\large&space;\vec{T}=-\vec{N}\sqrt{1-\frac{n_{1}^{2}}{n_{2}^{2}}*sin^{2}\theta&space;_{1}}&plus;\frac{n_{1}}{n_{2}}*\left&space;[&space;\vec{I}&plus;\left&space;(&space;-\vec{I}*\vec{N}&space;\right&space;)*\vec{N}&space;\right&space;]" title="\large \vec{T}=-\vec{N}\sqrt{1-\frac{n_{1}^{2}}{n_{2}^{2}}*sin^{2}\theta _{1}}+\frac{n_{1}}{n_{2}}*\left [ \vec{I}+\left ( -\vec{I}*\vec{N} \right )*\vec{N} \right ]" /></a>

<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{120}&space;\large&space;\vec{T}=-\vec{N}\sqrt{1-\frac{n_{1}^{2}}{n_{2}^{2}}\cdot\left&space;(&space;1-cos^{2}\theta_{1}&space;\right&space;)}&plus;\frac{n_{1}}{n_{2}}\cdot\left&space;[&space;\vec{I}&plus;\left&space;(&space;-\vec{I}\cdot\vec{N}&space;\right&space;)\cdot\vec{N}&space;\right&space;]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{120}&space;\large&space;\vec{T}=-\vec{N}\sqrt{1-\frac{n_{1}^{2}}{n_{2}^{2}}\cdot\left&space;(&space;1-cos^{2}\theta_{1}&space;\right&space;)}&plus;\frac{n_{1}}{n_{2}}\cdot\left&space;[&space;\vec{I}&plus;\left&space;(&space;-\vec{I}\cdot\vec{N}&space;\right&space;)\cdot\vec{N}&space;\right&space;]" title="\large \vec{T}=-\vec{N}\sqrt{1-\frac{n_{1}^{2}}{n_{2}^{2}}\cdot\left ( 1-cos^{2}\theta_{1} \right )}+\frac{n_{1}}{n_{2}}\cdot\left [ \vec{I}+\left ( -\vec{I}\cdot\vec{N} \right )\cdot\vec{N} \right ]" /></a>
<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{120}&space;\large&space;\vec{T}=-\vec{N}\sqrt{1-\frac{n_{1}^{2}}{n_{2}^{2}}\cdot\left&space;(&space;1-cos^{2}\theta_{1}&space;\right&space;)}&plus;\frac{n_{1}}{n_{2}}\cdot\left&space;[&space;\vec{I}-\left&space;(&space;\vec{I}\cdot\vec{N}&space;\right&space;)\cdot\vec{N}&space;\right&space;]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{120}&space;\large&space;\vec{T}=-\vec{N}\sqrt{1-\frac{n_{1}^{2}}{n_{2}^{2}}\cdot\left&space;(&space;1-cos^{2}\theta_{1}&space;\right&space;)}&plus;\frac{n_{1}}{n_{2}}\cdot\left&space;[&space;\vec{I}-\left&space;(&space;\vec{I}\cdot\vec{N}&space;\right&space;)\cdot\vec{N}&space;\right&space;]" title="\large \vec{T}=-\vec{N}\sqrt{1-\frac{n_{1}^{2}}{n_{2}^{2}}\cdot\left ( 1-cos^{2}\theta_{1} \right )}+\frac{n_{1}}{n_{2}}\cdot\left [ \vec{I}-\left ( \vec{I}\cdot\vec{N} \right )\cdot\vec{N} \right ]" /></a>

<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{120}&space;\large&space;\vec{T}=-\vec{N}\sqrt{1-\frac{n_{1}^{2}}{n_{2}^{2}}\cdot\left&space;[&space;1-\left&space;(&space;\vec{I}\cdot\vec{N}&space;\right&space;)^{2}&space;\right&space;]}&plus;\frac{n_{1}}{n_{2}}\cdot\left&space;[&space;\vec{I}-\left&space;(&space;\vec{N}\cdot\vec{I}&space;\right&space;)\cdot\vec{N}&space;\right&space;]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{120}&space;\large&space;\vec{T}=-\vec{N}\sqrt{1-\frac{n_{1}^{2}}{n_{2}^{2}}\cdot\left&space;[&space;1-\left&space;(&space;\vec{I}\cdot\vec{N}&space;\right&space;)^{2}&space;\right&space;]}&plus;\frac{n_{1}}{n_{2}}\cdot\left&space;[&space;\vec{I}-\left&space;(&space;\vec{N}\cdot\vec{I}&space;\right&space;)\cdot\vec{N}&space;\right&space;]" title="\large \vec{T}=-\vec{N}\sqrt{1-\frac{n_{1}^{2}}{n_{2}^{2}}\cdot\left [ 1-\left ( \vec{I}\cdot\vec{N} \right )^{2} \right ]}+\frac{n_{1}}{n_{2}}\cdot\left [ \vec{I}-\left ( \vec{N}\cdot\vec{I} \right )\cdot\vec{N} \right ]" /></a>

调换位置：

<a href="https://www.codecogs.com/eqnedit.php?latex=\dpi{120}&space;\large&space;\vec{T}=\frac{n_{1}}{n_{2}}\cdot\left&space;[&space;\vec{I}-\left&space;(&space;\vec{N}\cdot\vec{I}&space;\right&space;)\cdot\vec{N}&space;\right&space;]-\vec{N}\sqrt{1-\frac{n_{1}^{2}}{n_{2}^{2}}\cdot\left&space;[&space;1-\left&space;(&space;\vec{I}\cdot\vec{N}&space;\right&space;)^{2}&space;\right&space;]}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\dpi{120}&space;\large&space;\vec{T}=\frac{n_{1}}{n_{2}}\cdot\left&space;[&space;\vec{I}-\left&space;(&space;\vec{N}\cdot\vec{I}&space;\right&space;)\cdot\vec{N}&space;\right&space;]-\vec{N}\sqrt{1-\frac{n_{1}^{2}}{n_{2}^{2}}\cdot\left&space;[&space;1-\left&space;(&space;\vec{I}\cdot\vec{N}&space;\right&space;)^{2}&space;\right&space;]}" title="\large \vec{T}=\frac{n_{1}}{n_{2}}\cdot\left [ \vec{I}-\left ( \vec{N}\cdot\vec{I} \right )\cdot\vec{N} \right ]-\vec{N}\sqrt{1-\frac{n_{1}^{2}}{n_{2}^{2}}\cdot\left [ 1-\left ( \vec{I}\cdot\vec{N} \right )^{2} \right ]}" /></a>

此式与书中代码所表达的意思相同，Q.E.D
