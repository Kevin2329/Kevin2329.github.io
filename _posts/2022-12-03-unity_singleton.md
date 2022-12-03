---
layout: post
title: "在Unity中使用单例模式出现的问题"
date:   2022-12-03
tags: [Unity,DesignPattern,C#]
comments: true
author: Kevin
---

- 今天正在用单例模式写一个背包系统。简要代码如下：

<!-- more -->





```csharp
public class BagManager:MonoBehaviour
{
    public GameObject GridParent;
    private static BagManager _instance;
    public static BagManager Instance
    {
        get
        {
            if(_instance==null)
                _instance=new BagManager();
            return _instance;
        }
    }
}
```
当我在别处调用BagManager.Instance时，发现GridParent为null。调试了许久之后，我明白了。
此单例类BagManager挂载在场景的物体上，随着Play mode的进入，__BagManager已经被初始化，但是此时instance仍然为null__。外部调用BagManager.Instance时，根据以上代码，会再次new一个BagManager(),所以原本绑定的public变量GridParent就失效了。改成以下代码即可

```csharp
public class BagManager : MonoBehaviour
{
    public GameObject GridParent;

    private static BagManager _instance;
    public static BagManager Instance
    {
        get
        {
            return _instance;
        }
    }
    private void Awake()
    {
        _instance = this;
    }
```
因为该脚本挂载在物体上，在游戏开始时就会被初始化，所以只要在awake里让_instance等于自身就好了，代码中不用出现"new"这个关键词了。为了使得该代码更加健壮，将构造函数设置为private,放置在外部new。set也设置为private，防止在外部设置该值。
```csharp
public class BagManager : MonoBehaviour
{
    public GameObject GridParent;

    private BagManager(){}
    private static BagManager _instance;
    public static BagManager Instance
    {
        get
        {
            return _instance;
        }
        private set{}
    }
    private void Awake()
    {
        _instance = this;
    }
```