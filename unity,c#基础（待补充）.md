

 

# ·unity中c#的基本语法 



## 一.c#与c中变量的不同：

1.声明变量前带有"public" "private"区分公共和私有变量

2.bool类型的变量定义时默认为false

3.使用日志或语句输出文字:

```c#
Debug.Log();
outputText.text="";
```

4.输入:

```c#
Input.get___(Keycode._)
```



## 二.预制命令（函数）：

1.

```c#
Start()
```

每次play后立即执行

2.

```c#
Update()
```

每帧都执行

3.

```c#
Awake()
```

script是否启动都在开始时运行

....

[事件函数的执行顺序 - Unity 手册](https://docs.unity.cn/cn/2020.3/Manual/ExecutionOrder.html)

## 三.类

- [GameObject](https://docs.unity.cn/cn/2020.3/Manual/class-GameObject.html)：表示可以存在于场景中的对象的类型。
- [MonoBehaviour](https://docs.unity.cn/cn/2020.3/Manual/class-MonoBehaviour.html)：基类，默认情况下，所有 Unity 脚本都派生自该类。
- [Object](https://docs.unity.cn/cn/2020.3/Manual/class-Object.html)：Unity 可以在编辑器中引用的所有对象的基类。
- [Transform](https://docs.unity.cn/cn/2020.3/Manual/ScriptingTransform.html)：提供多种方式来通过脚本处理游戏对象的位置、旋转和缩放，以及与父和子游戏对象的层级关系。
- [Vectors](https://docs.unity.cn/cn/2020.3/Manual/VectorCookbook.html)：用于表达和操作 2D、3D 和 4D 点、线和方向的类。
- [Quaternion](https://docs.unity.cn/cn/2020.3/Manual/class-Quaternion.html)：表示绝对或相对旋转的类，并提供创建和操作它们的方法。
- [ScriptableObject](https://docs.unity.cn/cn/2020.3/Manual/class-ScriptableObject.html)：可用于保存大量数据的数据容器。
- [Time（以及帧率管理）](https://docs.unity.cn/cn/2020.3/Manual/TimeFrameManagement.html)：Time 类用于测量和控制时间，并管理项目的帧率。
- [Mathf](https://docs.unity.cn/cn/2020.3/Manual/class-Mathf.html)：一组常见的数学函数，包括三角函数、对数函数以及游戏和应用开发中常用的其他函数。
- [Random](https://docs.unity.cn/cn/2020.3/Manual/class-Random.html)：提供简便的方法来生成各种常用类型的随机值。
- [Debug](https://docs.unity.cn/cn/2020.3/Manual/class-Debug.html)：用于可视化编辑器中的信息，这些信息可以帮助您了解或调查项目运行时发生的情况。
- [Gizmos 和 Handles](https://docs.unity.cn/cn/2020.3/Manual/GizmosAndHandles.html)：用于在 Scene 视图和 Game 视图绘制线条和形状以及交互式手柄和控件。

#### 
