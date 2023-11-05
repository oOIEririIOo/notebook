# 从死亡动画中理解代码的父子级关系以及调用（clss调用）

在“小狐狸”实例中，每一个敌人都需要消灭动画，因此可以单独做一个类。

## 父级类：Enemy

 ·创建一个仅限于父子集关系中才能使用的变量

```c#
protected Animator anim;
protected virtual void Start()//virtual，override可以使父级的组件和子集互相改变
{
    
    anim = GetComponent<Animator>();
}
public void Death()
{
    Destroy(gameObject);
}
public void JumpOn()
{
    anim.SetTrigger("death");
}
```



## 子集类：Enemy_Frog

```c#
public class Enemy_Frog : Enemy
protected override void Start()//virtual，override可以使父级的组件和子集互相改变
{
    base.start();//获得父级start函数的内容
    
}
```

## 当第三物体需要调用该父子内容时

```c#
Enemy enemy = collision.gameObject.GetComponent<Enemy>();
```

