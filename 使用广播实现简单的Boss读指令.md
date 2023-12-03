# 使用广播实现简单的Boss读指令

不能打断回血的Boss不是好Boss。

## 1.新建一个void类型的SO

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

![image-20231127221157481](C:\Users\Eriri\AppData\Roaming\Typora\typora-user-images\image-20231127221157481.png)

## 2.声明新事件，并在按下回复后使用事件

```c#
public UnityEvent playerBehavior;
```

![image-20231127221232527](C:\Users\Eriri\AppData\Roaming\Typora\typora-user-images\image-20231127221232527.png)

```c#
 private void Healing(InputAction.CallbackContext context)
 {
     if (isSkill == false && physicsCheck.isGround && !playerController.isDead && !playerController.isHurt && !playerController.isDash)
     {
         playerBehavior?.Invoke(); 
     }
 }
```



## 3.在Boss挂载的脚本中接受广播

```c#
public VoidEventSO buffEvent;


 protected override void OnEnable()
 {
     base.OnEnable();
     buffEvent.OnEventRaised += OnBuffEvent;
 }



 protected override void OnDisable()
 {
     base.OnDisable();
     buffEvent.OnEventRaised -= OnBuffEvent;
 }
 
 private void OnBuffEvent()
 {
     if(currentState == walkToAttackState || currentState == walkToSpinAttackState || currentState == walkToLeapState)//只在walk状态中读取玩家指令
    SwitchState(BossStateType.Jump);//下一步新建跳跃状态
 }
```

## 4.新建跳跃状态，接受广播后Boss进入该状态

```c#
public class UncleJumpState : BossState
{
    private AnimatorStateInfo info;
    public override void OnEnter(BossFSM enemy)
    {
        currentEnemy = enemy;
        currentEnemy.anim.Play("Jump");
    }
    public override void LogicUpdate(BossFSM enemy)
    {
        
    }

    public override void PhysicsUpdate()
    {
        info = currentEnemy.anim.GetCurrentAnimatorStateInfo(0);
        if (info.normalizedTime >= 0.9f)
        {
            currentEnemy.SwitchState(BossStateType.WalkToAttack);
        }
    }

    public override void OnExit()
    {

    }

}

```

## 5.使用动画事件，在FixedUpdate中让Boss位移到玩家所在位置

```c#
public bool dashStart;

 public void DashToPlayer()//在动画事件中控制
 {

     dashStart = true;
     
 }

 public void DashToPlayerFinish()//在动画事件中控制
 {
     dashStart = false;
 }



protected virtual void FixedUpdate()
{
    currentState.PhysicsUpdate();
    if(dashStart)
    {
        transform.position = Vector2.Lerp(transform.position, target.transform.position, 0.05f);
    }
}
```

