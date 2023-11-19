# 在Unity中使用状态机制作一个敌人AI

参考：BV1zf4y1r7FJ、BV1xp4y137Xr

## 1.创建接口代码

```c#
public abstract class IState
{
    protected FSM currentEnemy;
    public abstract void OnEnter(FSM enemy);

    public abstract void LogicUpdate();

    public abstract void PhysicsUpdate();

    public abstract void OnExit();
}

```

## 2.创建状态机脚本用于导入敌人

```c#
//创建枚举类型储存状态
public enum StateType
{
    Idle, Patrol, Chase, React, Attack
}
//////////////////



public class FSM : MonoBehaviour
    protected virtual void Awake()
{
    
}

private void OnEnable()
{
    currentState = idleState;
    currentState.OnEnter(this);
}

private void Update()
{
    currentState.LogicUpdate();
   
}

private void FixedUpdate()
{
    currentState.PhysicsUpdate();
}

private void OnDisable()
{
    currentState.OnExit();
}


public void SwitchState(StateType state)  //切换状态
{
    var newState = state switch
    {
        StateType.Idle => idleState,
        StateType.Patrol => patrolState,
        StateType.Chase => chaseState,
        StateType.Attack => attackState,
        StateType.React => reactState,
        _ => null
    };

    currentState.OnExit();
    currentState = newState;
    currentState.OnEnter(this);
}
```

## 3.创建敌人脚本继承状态机并导入状态

```c#
public class Skeleton : FSM
{
    protected override void Awake()
    {
        base.Awake();
        idleState = new SkeletonIdleState();
        patrolState = new SkeletonPatrolState();
        chaseState = new SkeletonChaseState();
        attackState = new SkeletonAttackState();
        reactState = new SkeletonReactState();
    }
}
```



## 4.创建单独敌人的状态脚本

```c#
public class SkeletonIdleState : IState //Idle状态

{

    private float IdleTime = 0f;
    public override void OnEnter(FSM enemy)
    {
        currentEnemy = enemy;
        
    }
    public override void LogicUpdate()
    {
        
    }

    public override void PhysicsUpdate()
    {
        
    }

    public override void OnExit()
    {
        
    }

}
//除此之外还有：
public class SkeletonPatrolState : IState
public class SkeletonChaseState : IState
public class SkeletonAttackState : IState
public class SkeletonReactState : IState
//.................
```

