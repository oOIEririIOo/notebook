# ScriptableObject的运用

## 																					广播---->中转---->接收

## 1.创建 ScriptableObject类进行广播和接收

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Events;


[CreateAssetMenu(menuName = "Event/VoidEventSO")]
public class VoidEventSO : ScriptableObject
{
    public UnityAction OnEventRaised;

    public void RaiseEvent()
    {
        OnEventRaised?.Invoke();
    }
}

```

## 并创建asset文件存放

![image-20231119155349840](C:\Users\Eriri\AppData\Roaming\Typora\typora-user-images\image-20231119155349840.png)

## 2.在事件中广播数据：

![image-20231119155858108](C:\Users\Eriri\AppData\Roaming\Typora\typora-user-images\image-20231119155858108.png)

## 3.订阅事件并接收

```c#
 private void OnEnable()
 {
     cameraShakeEvent.OnEventRaised += OnCameraShakeEvent;
 }
private void OnDisable()
{
    cameraShakeEvent.OnEventRaised -= OnCameraShakeEvent;
}

 private void OnCameraShakeEvent()
 {
     //impulseSource.GenerateImpulse();
 }
```

