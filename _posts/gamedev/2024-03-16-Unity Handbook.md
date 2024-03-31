---
title: Unity Handbook
categories: GameDev
tags:
- GameDev
---

- [教程项目](#教程项目)
  - [Junior Programmer](#junior-programmer)
    - [CWC 1](#cwc-1)
      - [CWC 1 Unit 1 - Player Control](#cwc-1-unit-1---player-control)
      - [CWC 1 Unit 2 - Basic Gameplay](#cwc-1-unit-2---basic-gameplay)
      - [CWC 1 Bonus Features 2](#cwc-1-bonus-features-2)
      - [CWC 2 Challenge 2 - Play Fetch](#cwc-2-challenge-2---play-fetch)
      - [CWC 1 Bonus Features 2](#cwc-1-bonus-features-2-1)
      - [CWC 1 Mod the Cube (纯脚本设置参数)](#cwc-1-mod-the-cube-纯脚本设置参数)
      - [CWC 1 Personal Project](#cwc-1-personal-project)
    - [CWC 2 Unit 3 - Sound and Effects](#cwc-2-unit-3---sound-and-effects)
      - [背景设置](#背景设置)
      - [调用 player’s Rigidbody 实现跳跃](#调用-players-rigidbody-实现跳跃)
      - [防止双跳(double-jumping)](#防止双跳double-jumping)
      - [有碰撞体积的障碍物Prefab， 向player方向translate](#有碰撞体积的障碍物prefab-向player方向translate)
      - [SpawnManager](#spawnmanager)
      - [限制Player的pos](#限制player的pos)
      - [重复背景](#重复背景)
      - [碰撞触发Game Over, 停止相关代码](#碰撞触发game-over-停止相关代码)
      - [探索 Player 的 Animations](#探索-player-的-animations)
      - [设置 Jump 动画](#设置-jump-动画)
      - [调整 Jump 动画](#调整-jump-动画)
      - [设置撞击倒地动画](#设置撞击倒地动画)
      - [防止倒地后还能跳跃](#防止倒地后还能跳跃)
      - [自定义爆炸粒子](#自定义爆炸粒子)
      - [在碰撞时播放粒子](#在碰撞时播放粒子)
      - [添加污垢飞溅颗粒](#添加污垢飞溅颗粒)
      - [向相机对象添加音乐](#向相机对象添加音乐)
      - [向 Player 添加音效](#向-player-添加音效)
    - [CWC 2 Challenge 3 - Balloons, Bombs, \& Booleans](#cwc-2-challenge-3---balloons-bombs--booleans)
    - [CWC 2 Lab 3 - Player Control](#cwc-2-lab-3---player-control)
      - [3.Constrain the Player’s movement](#3constrain-the-players-movement)
    - [CWC 2 Unit 4 - Gameplay Mechanics](#cwc-2-unit-4---gameplay-mechanics)
      - [3.Create a focal point for the camera](#3create-a-focal-point-for-the-camera)
      - [4.Rotate the focal point by user input](#4rotate-the-focal-point-by-user-input)
      - [5.Add forward force to the player](#5add-forward-force-to-the-player)
      - [6.Move in direction of focal point](#6move-in-direction-of-focal-point)
  - [Unity Essentials](#unity-essentials)
      - [Render mode](#render-mode)
      - [Scene操作](#scene操作)
      - [Camera Projection](#camera-projection)
      - [LateUpdate() 和 Update()](#lateupdate-和-update)
      - [玩家控制输入](#玩家控制输入)
      - [边界限制](#边界限制)
- [Handbook](#handbook)
  - [2D 项目](#2d-项目)
      - [Layer](#layer)
      - [Pos固定](#pos固定)
- [项目及团队](#项目及团队)
  - [流程](#流程)
      - [游戏设计文档](#游戏设计文档)
      - [生产](#生产)
      - [后期制作](#后期制作)
      - [GDD](#gdd)
      - [项目管理](#项目管理)
      - [项目章程 Project Charter](#项目章程-project-charter)
      - [管理项目，项目跟踪器](#管理项目项目跟踪器)
    - [测试](#测试)
      - [错误报告的艺术](#错误报告的艺术)
    - [运营](#运营)
      - [项目回顾](#项目回顾)
- [DCC](#dcc)
      - [3D 资源获取](#3d-资源获取)
      - [2D 资源](#2d-资源)
      - [音频资源获取](#音频资源获取)
    - [Audio](#audio)
        - [3D 音效](#3d-音效)


# 教程项目

## Junior Programmer

### CWC 1

#### CWC 1 Unit 1 - Player Control

1. asset导入：从Unity的顶部菜单中，选择`Assets > Import Package > Custom Package`, 选择unitypackage
2. Obj聚焦：`press F` to focus on it
3. 按住 `Ctrl/Cmd` 以整单位移动相机
4. 布局：在右上角，选layout 或 自定义layout保存


#### CWC 1 Unit 2 - Basic Gameplay
1. 选择 Material, 拖拽到obj以apply

2. 获取用户的水平输入

```cs
public float horizo​​ntalInput;

void Update() {
    Horizo​​ntalInput = Input.GetAxis(“Horizo​​ntal”) ;
}

```

3. Translate

```cs
    /// <summary>
    ///   <para>Moves the transform in the direction and distance of translation.</para>
    /// </summary>
    /// <param name="translation"></param>
    /// <param name="relativeTo"></param>
    public void Translate(Vector3 translation)
```

4. 保持obj在边界内

```cs
void Update() {
    var currentPosition = transform.position;
    if (currentPosition.x > bound) {
        transform.position = new Vector3(bound, currentPosition.y, currentPosition.z);
    }
}
```


#### CWC 1 Bonus Features 2
[Doc](https://learn.unity.com/tutorial/bonus-features-2-share-your-work#)

#### CWC 2 Challenge 2 - Play Fetch
[Doc](https://learn.unity.com/tutorial/challenge-2-play-fetch-with-random-values-and-arrays#)

1. SpawnManager

2. GameObj destroy

3. Random spawn

4. InvokeRepeating

```cs
    /// <summary>
    ///   <para>Invokes the method methodName in time seconds, then repeatedly every repeatRate seconds.</para>
    /// </summary>
    /// <param name="methodName">The name of a method to invoke.</param>
    /// <param name="time">Start invoking after n seconds.</param>
    /// <param name="repeatRate">Repeat every n seconds.</param>
    public void InvokeRepeating(string methodName, float time, float repeatRate)
    {
      if ((double) repeatRate <= 9.999999747378752E-06 && (double) repeatRate != 0.0)
        throw new UnityException("Invoke repeat rate has to be larger than 0.00001F)");
      MonoBehaviour.InvokeDelayed(this, methodName, time, repeatRate);
    }
```

5. CoolDownTime

```cs
using System.Collections;
using UnityEngine;

public class Player : MonoBehaviour
{
    // 冷却时间
    public float cooldownTime = 2f;
    // 上次执行方法的时间
    private float lastExecutionTime = 0f;

    void Update()
    {
        // 在 Update 方法中检查按键输入并调用方法
        if (Input.GetKeyDown(KeyCode.Space))
        {
            // 检查是否已经超过冷却时间
            if (Time.time - lastExecutionTime >= cooldownTime)
            {
                // 调用方法
                MyMethod();

                // 更新上次执行时间为当前时间
                lastExecutionTime = Time.time;
            }
        }
    }

    void MyMethod()
    {
        // 这是你想要添加冷却时间的方法的内容
        Debug.Log("Method executed!");
    }
}
```

#### CWC 1 Bonus Features 2
1. SpawnManager 随机地点随机方向生成

```cs
public class SpawnManager : MonoBehaviour
{
    // 可在Unity编辑器中指定的动物预制体数组
    public GameObject[] animalPrefabs;

    // 饥饿条的Prefab
    public GameObject healthBarPrefab;

    // 场景边界的常量值
    private const float Bound = 30f;

    // 开始生成动物的延迟时间
    private const float StartDelay = 2;

    // 生成动物的时间间隔
    private const float SpawnInterval = 5.0f;

    // 在游戏对象创建时调用，用于初始化
    private void Start()
    {
        // 调用InvokeRepeating方法，在指定的延迟后开始重复执行指定的方法
        // 第一个参数："SpawnRandomAnimal" 是要重复调用的方法的名称（字符串）
        // 第二个参数：startDelay 是延迟开始重复调用的时间（以秒为单位）
        // 第三个参数：spawnInterval 是重复调用的时间间隔（以秒为单位）        
        InvokeRepeating(nameof(SpawnRandomAnimal), StartDelay, SpawnInterval);
    }

    // 每帧调用一次
    private void Update()
    {
    }

    // 生成随机动物的方法
    private void SpawnRandomAnimal()
    {
        // 随机选择一个动物预制体
        int animalIndex = Random.Range(0, animalPrefabs.Length);

        // 计算生成位置
        Vector3 spawnPos = CalculateSpawnPosition();

        // 计算生成的旋转方向
        Quaternion rotation = CalculateRotation(spawnPos);

        // 实例化生成动物
        GameObject newAnimal = Instantiate(animalPrefabs[animalIndex], spawnPos, rotation);
    }

    // 计算生成位置的方法
    private static Vector3 CalculateSpawnPosition()
    {
        // 在场景边界范围内随机生成位置
        var x = Random.Range(-Bound, Bound);
        var z = Random.Range(-Bound, Bound);

        // 随机选择沿着x轴或z轴生成
        var alongX = Random.Range(0, 2) == 0;
        if (alongX)
        {
            z = Bound * (Random.Range(0, 2) == 0 ? 1 : -1);
        }
        else
        {
            x = Bound * (Random.Range(0, 2) == 0 ? 1 : -1);
        }

        return new Vector3(x, 0, z);
    }

    // 计算生成旋转方向的方法
    private static Quaternion CalculateRotation(Vector3 spawnPos)
    {
        // 计算指向场景中心的方向
        var directionToCenter = Vector3.zero - spawnPos;
        // 生成以该方向为前方向的旋转
        var rotation = Quaternion.LookRotation(directionToCenter, Vector3.up);
        return rotation;
    }
}
```

2. GameManager 多个脚本间通信

```cs
public class GameManager : MonoBehaviour
{
    private int score = 0;
    private int lives = 3;
    // Start is called before the first frame update
    void Start() {}

    // Update is called once per frame
    void Update() {}
    
    public void AddLives(int value)
    {
        lives += value;
        if (lives <= 0)
        {
            Debug.Log("Game Over");
            lives = 0;
        }
        Debug.Log("Lives = " + lives);
    }
    
    public void AddScore(int value)
    {
        score += value;
        Debug.Log("Score = " + score);
    }
}
```

在其他脚本中使用gameManager

```cs
public class Other : MonoBehaviour
{
    private GameManager gameManager;
    // Start is called before the first frame update
    void Start()
    {
        gameManager = GameObject.Find("GameManager").GetComponent<GameManager>();
    }
}
```


3. Collider 碰撞, Trigger

- 判断碰撞obj： `CompareTag()`
- obj调用自己的方法： `other.GetComponent<AnimalHunger>().FeedAnimal(1)`

```cs
public class DetectCollisions : MonoBehaviour
{
    private GameManager gameManager;
    // Start is called before the first frame update
    void Start()
    {
        gameManager = GameObject.Find("GameManager").GetComponent<GameManager>();
    }

    // Update is called once per frame
    void Update()
    {

    }

    /// <summary>
    /// 当碰撞器与其他碰撞器发生接触时调用此方法。
    /// </summary>
    /// <param name="other">与该碰撞器发生接触的另一个碰撞器。</param>
    void OnTriggerEnter(Collider other)
    {
        // 检查与碰撞器发生接触的其他对象是否被标记为"Player"
        if (other.CompareTag("Player"))
        {
            // 如果是"Player"对象，则调用GameManager的AddLives方法减少生命值，并销毁GameManager对象
            gameManager.AddLives(-1);
            Destroy(gameManager);
        } 
        // 检查与碰撞器发生接触的其他对象是否被标记为"Animal"
        else if (other.CompareTag("Animal"))
        {
            // 如果是"Animal"对象，则获取AnimalHunger组件，并调用FeedAnimal方法喂养动物，增加游戏分数，并销毁当前游戏对象
            other.GetComponent<AnimalHunger>().FeedAnimal(1);
            gameManager.AddScore(5);
            Destroy(gameObject);
        }
    }
}
```

> !!Note!!: 在Unity中，如果你使用的是物理系统（Physics System），当两个物体发生碰撞或进入触发器时，`至少一个物体需要拥有刚体组件`才能触发碰撞或触发事件。

> 例如，如果你想要在两个物体之间触发碰撞事件，其中一个物体必须拥有刚体组件，而另一个物体可以是一个普通的碰撞器，不需要刚体组件。

>通常来说，将刚体组件添加到动态移动的物体上，而将碰撞器组件添加到静止的物体上是比较常见的做法。


4. 基于UI与prefab的饥饿条

- UI-Slider
- 为animal prefab 添加 slider prefab ： [Doc](https://connect-prd-cdn.unity.com/20210505/70ffeabd-706f-4556-b9a9-ea6bd8ba631a/Unit%202%20-%20Bonus%20Features%20Solutions.pdf?_ga=2.263578828.1186801097.1620052249-59568313.1601905412) 从p32开始看

```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;

public class AnimalHunger : MonoBehaviour
{
    public Slider hungerSlider;
    public int amountToBeFed;
    private int currentFedAmount = 0;
    private GameManager gameManager;

    // Start is called before the first frame update
    void Start()
    {
        // 设置饥饿滑块的最大值为要喂养的量
        hungerSlider.maxValue = amountToBeFed;

        // 设置饥饿滑块的最小值为0
        hungerSlider.minValue = 0;

        // 禁用饥饿滑块的填充对象
        // 将对象的活动状态设置为假，即禁用该对象的渲染和碰撞功能。
        hungerSlider.fillRect.gameObject.SetActive(false);

        // 查找名为"GameManager"的游戏对象，并获取其GameManager组件
        gameManager = GameObject.Find("GameManager").GetComponent<GameManager>();
    }


    // Update is called once per frame
    void Update()
    {
    }

    public void FeedAnimal(int amount)
    {
        // 给动物喂食的方法，参数为喂食的数量

        // 增加当前喂食总量
        currentFedAmount += amount;

        // 激活饥饿滑块的填充物体
        hungerSlider.fillRect.gameObject.SetActive(true);

        // 更新饥饿滑块的值
        hungerSlider.value = currentFedAmount;

        // 如果当前喂食总量达到或超过需要喂食的总量
        if (currentFedAmount >= amountToBeFed)
        {
            // 调用游戏管理器的方法，增加分数（传入需要喂食的总量作为参数）
            gameManager.AddScore(amountToBeFed);

            // 销毁当前游戏对象（延迟0.1秒后销毁）
            Destroy(gameObject, 0.1f);
        }
    }
}
```


#### CWC 1 Mod the Cube (纯脚本设置参数)

- Transform
- Material opacity


```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Cube : MonoBehaviour
{
    // 渲染器
    public MeshRenderer Renderer;
    // 材质
    private Material _material;
    // 不透明度
    private float _opacity;
    // 不透明度变化方向
    private float _opacityDirection;

    void Start()
    {
        // 设置初始位置
        transform.position = new Vector3(0, 0, 0);
        // 设置初始缩放
        transform.localScale = Vector3.one * 1.3f;
        // 设置初始旋转
        transform.rotation = Quaternion.Euler(Random.Range(0, 360), Random.Range(0, 360), Random.Range(0, 360));

        // 获取渲染器的材质
        _material = Renderer.material;
        // 初始化不透明度
        _opacity = 0f;
        // 初始化不透明度变化方向
        _opacityDirection = 1f;
        // 设置初始颜色和不透明度
        _material.color = new Color(0.5f, 1.0f, 0.3f, _opacity);
    }

    void Update()
    {
        // 设置旋转速度
        var rotateSpeed = Random.Range(0f, 360f);
        // 绕各轴旋转
        transform.Rotate(rotateSpeed * Time.deltaTime, rotateSpeed * Time.deltaTime, rotateSpeed * Time.deltaTime);
        
        // 周期性改变不透明度
        PeriodicalChangeOpacity();
    }

    void PeriodicalChangeOpacity()
    {
        // 根据不透明度的当前值确定不透明度的变化方向
        _opacityDirection = _opacity switch
        {
            // 当不透明度接近 1 时，使其减小
            > 0.9f => -0.0001f,
            // 当不透明度接近 0 时，使其增加
            < 0.1f => 0.0001f,
            // 其他情况不变
            _ => _opacityDirection
        };

        // 根据不透明度变化方向调整不透明度
        _opacity += _opacityDirection;
        // 更新材质的颜色和不透明度
        _material.color = new Color(0.5f, 1.0f, 0.3f, _opacity);
    }
}
```

#### CWC 1 Personal Project
1. primitive

2. camera视角的常用实践
- 对于一个自上而下的游戏，将摄像机定位在（0，10，0）正上方，并在X轴上旋转90度

- 对于侧视图游戏，在X轴上旋转平面—90度

- 对于第三人称视角游戏，在Y轴和Z轴向上移动摄像机，并在X轴上增加其旋转

3. 同时调节scale
提示：在Unity的较新版本中，您可以通过切换"启用约束比例"图标，同时设置所有轴上的比例。
![Enabled Constrained Proportions icon](https://unity-connect-prd.storage.googleapis.com/20231214/learn/images/c2f44eba-5971-4f3b-9463-5ca844720e89_image.png)

4. 保存项目，打包备份
- In the Project window, Right-click on the `“Assets” folder > Export Package`, then click Export

- Create a new “Backups” folder in your Personal Project folder, then save it with your name and the version number (e.g. Carl_V0.1.unitypackage”)

5. GetKey和GetKeyDown
Input.GetKey(string keyName)：

这个方法用于检测指定按键是否被按下。
当按键被按下并保持按住时，该方法会持续返回 true。
如果按键没有被按下，则返回 false。
这个方法会在每一帧都检测按键状态。


Input.GetKeyDown(string keyName)：

这个方法用于检测指定按键在当前帧是否被按下。
当按键在当前帧被按下时，该方法返回 true，但是在后续的帧中，即使按键保持按住，也不会再次返回 true。
如果按键在当前帧没有被按下，则返回 false。
这个方法只会在按键按下的那一帧返回 true，而在之后的帧中会返回 false。


举例来说，假设你想要在玩家按下空格键时触发某个动作：

如果你使用 Input.GetKey("space")，那么当玩家按下空格键后，该动作将在每一帧都触发，只要空格键一直被按住。
如果你使用 Input.GetKeyDown("space")，那么该动作将只在玩家按下空格键的那一帧触发，而不管玩家是否保持按住空格键。

6. Prefab override
如果您对场景中的预制件进行了更改，并希望将这些更改应用于所有预制件


### CWC 2 Unit 3 - Sound and Effects
在这个初级程序员任务中，你将扩展你的基础学习，并创建基本的自定义交互与Unity。

当您完成四个实际项目时，您将探索一系列支持基本功能的概念，包括:

**循环、数据类型、引用、脚本通信和UI。**

为了完成任务，您将为您的投资组合创建一个简单的原型应用程序。在此任务结束时，您将获得参加Unity Certified User：Programmer认证考试所需的所有技能。

在本单元中，您将编程一个快节奏的无休止的 横向卷轴 跑步者游戏，玩家需要时间跳过迎面而来的障碍物，以避免崩溃。

在创建此原型时，您将学习如何`添加音乐和音效`，从而彻底改变项目的体验。

您还将学习如何`创建动态无休止的重复背景`，这对任何侧滚动游戏都至关重要。

最后，您将学习加入`粒子效果`，如飞溅和爆炸，这使您的游戏更令人满意。

#### 背景设置

在层次结构中选择Background对象，然后在`Sprite Renderer component > Sprite，选择_City、_Nature或_Town`
![image](https://unity-connect-prd.storage.googleapis.com/20231214/learn/images/840375f1-defc-44da-95ec-10f8b6a0429d_image.png)

#### 调用 player’s Rigidbody 实现跳跃
   
- _playerRb.AddForce(Vector3.up * 100, ForceMode.Impulse):
    这行代码使用了 ForceMode.Impulse，表示施加的是一个瞬间的冲量。这意味着施加的力将会立即应用到刚体上，不受刚体当前速度的影响，而是立即改变刚体的速度。

- _playerRb.AddForce(Vector3.up * 100):
    这行代码没有指定施加的力的方式，默认情况下使用的是 ForceMode.Force，表示施加的是一个持续的力。这意味着施加的力会持续地应用到刚体上，会受到刚体当前速度的影响，并逐渐改变刚体的速度，直到力被移除或受到其他因素的影响。


#### 防止双跳(double-jumping)
- 通过布尔值和碰撞检测防止空中跳跃
- `OnCollisionEnter(Collision other)`

```cs
public class PlayerController : MonoBehaviour
{
    private Rigidbody _playerRb; // 用于存储玩家刚体组件的引用

    public float jumpForce; // 跳跃力大小
    public float gravityModifier; // 重力修正因子
    public bool isOnGround = true; // 标记玩家是否在地面上

    // Start is called before the first frame update
    void Start()
    {
        // 获取当前游戏对象（即此脚本所附加到的游戏对象）上的 Rigidbody 组件
        _playerRb = GetComponent<Rigidbody>();

        // 使用重力修正因子调整物理引擎设置的重力
        Physics.gravity *= gravityModifier;
    }

    // Update is called once per frame
    void Update()
    {
        // 检测是否按下空格键，并且玩家在地面上
        if (Input.GetKeyDown(KeyCode.Space) && isOnGround)
        {
            // 在玩家刚体上施加向上的冲量，冲量大小为 (0, jumpForce, 0)
            // ForceMode.Impulse 是施加力的方式，即瞬间施加一个冲量
            _playerRb.AddForce(Vector3.up * jumpForce, ForceMode.Impulse);
            isOnGround = false; // 标记玩家不在地面上
        }
    }

    /// <summary>
    /// OnCollisionEnter is called when this collider/rigidbody has begun touching another rigidbody/collider.
    /// This function can be a coroutine.
    /// </summary>
    /// <param name="collision"></param>
    private void OnCollisionEnter(Collision collision)
    {
        isOnGround = true; // 碰撞发生时，标记玩家在地面上
    }
}

```

#### 有碰撞体积的障碍物Prefab， 向player方向translate

```cs
public class MoveLeft : MonoBehaviour
{
    public float speed = 30f;
    // Start is called before the first frame update
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        transform.Translate(Vector3.left * (Time.deltaTime * speed));
    }
}
```

#### SpawnManager 

- 在固定位置生成障碍物prefab， 记得将控制prefab向左translate的脚本override
- extract 生成障碍物方法并InvokeRepeating 调用

```cs
public class SpawnManager : MonoBehaviour // 定义一个名为 SpawnManager 的类，继承自 MonoBehaviour 类
{
    public GameObject obstaclePrefab; // 公共字段，用于存储障碍物预制体的引用

    private Vector3 _spawnPos = new Vector3(25, 0, 0); // 私有字段，用于存储生成位置的坐标
    private float startDelay = 2; // 私有字段，表示生成障碍物的起始延迟时间
    private float repeatRate = 2; // 私有字段，表示生成障碍物的重复间隔时间
    
    // Start is called before the first frame update
    void Start() // 在游戏对象被启用时调用一次的方法
    {
        InvokeRepeating(nameof(SpawnObstacle), startDelay, repeatRate); // 以指定的延迟时间和重复间隔时间调用 SpawnObstacle 方法
    }

    // Update is called once per frame
    void Update() // 每帧调用一次的方法
    {
        // 此处留空，表示在 Update 方法中不执行任何逻辑操作
    }

    void SpawnObstacle() // 生成障碍物的方法
    {
        Instantiate(obstaclePrefab, _spawnPos, obstaclePrefab.transform.rotation); // 生成一个障碍物实例，并放置在指定位置和旋转角度
    }
}

```
   
#### 限制Player的pos

在player刚体组件中，展开constraints，然后冻结除Y position以外的所有

#### 重复背景
1. 将moveLeft.cs 应用于Background obj

2. 为了重复背景，并提供一个世界匆匆而过的错觉，我们需要重置背景对象的位置，使其完美地结合在一起。

3. 我们每隔几秒就重复一次背景，但过渡看起来很尴尬。我们需要使用一些新的变量来完美地和无缝地创建后台循环。
   - 通过获取背景collider的width来设置repeatWidth 获得更自然的效果 （其比例与背景图由多少重复构成，当然也可以自制倍数图）

```cs
public class RepeatBackground : MonoBehaviour
{
    private Vector3 _startPos; // 背景起始位置
    private float _repeatWidth; // 背景重复宽度的一半

    // Start is called before the first frame update
    void Start()
    {
        // 获取背景起始位置
        _startPos = transform.position;
        // 获取背景盒碰撞器的大小，并计算出背景重复宽度的一半(因为选用的background 是两帧重复)
        _repeatWidth = GetComponent<BoxCollider>().size.x / 2;
    }

    // Update is called once per frame
    void Update()
    {
        // 如果背景的 x 坐标小于起始位置 x 坐标减去重复宽度的一半
        if (transform.position.x < _startPos.x - _repeatWidth)
        {
            // 将背景位置重置为起始位置，实现背景的无限重复
            transform.position = _startPos;
        }
    }
}
```

#### 碰撞触发Game Over, 停止相关代码
当玩家与障碍物碰撞时，我们希望触发一个“游戏结束”状态，停止一切。为了做到这一点，我们需要一种方法来标记和识别玩家碰撞的所有游戏对象。

通过tag来判断player是在和ground碰撞还是和障碍物碰撞

```cs
public class PlayerController : MonoBehaviour
{
    // ...
    public bool isOnGround = true;
    public bool gameOver = false;
    
    // ...

    /// <summary>
    /// OnCollisionEnter is called when this collider/rigidbody has begun touching another rigidbody/collider.
    /// This function can be a coroutine.
    /// </summary>
    /// <param name="collision"></param>
    private void OnCollisionEnter(Collision collision)
    {
        if (collision.gameObject.CompareTag("Ground"))
        {
            isOnGround = true;
        }
        else if (collision.gameObject.CompareTag("Obstacle"))
        {
            gameOver = true;
            Debug.Log("Game Over!");
        }
    }
}
```

背景和物体在与障碍物碰撞时继续移动。我们需要MoveLeft脚本与PlayerController通信，并在玩家触发gameOver后停止。

```cs
public class MoveLeft : MonoBehaviour
{
    public float speed = 30f; // 速度参数，控制左移速度
    private PlayerController _playerControllerScript; // 对PlayerController脚本的引用
    private float _leftBound = -15;

    // Start is called before the first frame update
    void Start()
    {
        // 在开始时获取PlayerController脚本的引用
        _playerControllerScript = GameObject.Find("Player").GetComponent<PlayerController>(); 
    }

    // Update is called once per frame
    void Update()
    {
        if (!_playerControllerScript.gameOver) // 如果游戏未结束
        {
            // 将物体向左移动，速度由speed参数控制
            transform.Translate(Vector3.left * (Time.deltaTime * speed)); 
        }

        if (transform.position.x < _leftBound && gameObject.CompareTag("Obstacle"))
        {
            Destroy(gameObject);
        }
    }
}
```

当gameOver == true时，SpawnManager仍然在增加障碍物大军！我们需要与Spawn Manager脚本沟通，并告诉它在游戏结束时停止。

```cs
public class SpawnManager : MonoBehaviour
{
    public GameObject obstaclePrefab;

    private Vector3 _spawnPos = new Vector3(25, 0, 0);
    private float startDelay = 2;
    private float repeatRate = 2;
    private PlayerController _playerController;
    
    void Start()
    {
        InvokeRepeating(nameof(SpawnObstacle), startDelay, repeatRate);
        _playerController = GameObject.Find("Player").GetComponent<PlayerController>();
    }

    // ...

    void SpawnObstacle()
    {
        if (!_playerController.gameOver)
        {
            Instantiate(obstaclePrefab, _spawnPos, obstaclePrefab.transform.rotation);
        }
    }
}
```

#### 探索 Player 的 Animations
1. 双击Player 的 Animator 组件的 Controller，然后探索不同的Layer，
    进入Animator window后 各个 Layer 的 网格图，`可以 按住 option 拖拽以查看不同部分`


2. 其中各个框就是代表不同的 `State`
    双击 State 可以看动画效果的preview
    双击链接不同 state 的 arrow line和`各状态间转换的 condition`

3. 在 Animator Window， Layers tab 右侧有 Parameters tab, 将 Speed_f变量更改为1.0

4. 右键单击Run_Static> `Set as Layer Default State`

5. 单击Run_Static状态并调整 inspector 中的 `Speed = 1.5f` 值以匹配背景的速度


#### 设置 Jump 动画
State 中 Run => Running_Jump 有个 condition param : `"Jump_trig"`

```cs
public class PlayerController : MonoBehaviour
{
    
    // ...
    private Animator _playerAnimator;
    
    // Start is called before the first frame update
    void Start()
    {
        // ...
        
        _playerAnimator = GetComponent<Animator>();
        
        // ...
    }


    // Update is called once per frame
    void Update()
    {
        // 检测是否按下空格键
        if (Input.GetKeyDown(KeyCode.Space) && isOnGround)
        {
            // ... 
            
            // State : Run => Running_Jump condition : "Jump_trig"
            _playerAnimator.SetTrigger("Jump_trig");
        }
    }

}
```
> todo: SetTrigger trigger 是什么数据类型？

#### 调整 Jump 动画

1. 单击Running_Jump状态，然后在检查器中降低 `Speed = 0.7` 以减慢动画速度
2. 调整玩家的质量(60kg)、跳跃力(700)和gravityModifier(1.5)，让你的跳跃刚刚好

#### 设置撞击倒地动画

角色应该有一个动画。当它与物体碰撞时，角色应该像被击倒一样摔倒，而不是继续冲刺。

1. 在玩家与障碍物碰撞时，设置 `Death bool("Death_b")` 为真
2. 在同一个if语句中，将 `DeathType(DeathType_int)` 设置为1

```cs
public class PlayerController : MonoBehaviour
{

    private void OnCollisionEnter(Collision collision)
    {
        if (collision.gameObject.CompareTag("Ground"))
        {
            // ...
        }
        else if (collision.gameObject.CompareTag("Obstacle"))
        {
            // ...   
            _playerAnimator.SetBool("Death_b", true);
            _playerAnimator.SetInteger("DeathType_int", 1);
        }
    }
}
```

#### 防止倒地后还能跳跃

```cs
    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space) && isOnGround && !gameOver) // 添加gameover检测
        {
            _playerRb.AddForce(Vector3.up * jumpForce, ForceMode.Impulse);
            isOnGround = false;
            
            _playerAnimator.SetTrigger("Jump_trig");
        }
    }
```

#### 自定义爆炸粒子
1. From the `Course Library > Particles`, drag `FX_Explosion_Smoke` into the hierarchy, then use the `Play / Restart / Stop` buttons to preview it
   1. `Play / Restart / Stop` 在 Scene window 右下部
2. Play around with the `settings` to get your `particle system` the way you want it
   1. Inspector -> Particle System -> Velocity over lifeTime -> speed Modifier
3. Make sure to uncheck the `Play on Awake` setting
   1. Inspector -> Particle System -> Play On Awake
   2. 设置为true会让该粒子效果在游戏开始就触发
4. Drag the `particle` onto your player to make it a `child object`, then position it relative to the player 
   1. 让例子效果成为Player的子obj


#### 在碰撞时播放粒子
1. In `PlayerController.cs`, declare a new `public ParticleSystem explosionParticle`;
2. In the Inspector, assign the `explosion` to the `explosion particle` variable
   1. 从 Hierarchy -> Player 的 child Object 拖 `FX_Explosion_Smoke`
3. In the if-statement where the player collides with an obstacle, call `explosionParticle.Play()`;, then test and tweak the `particle properties`

```cs
public class PlayerController : MonoBehaviour
{

    public ParticleSystem explosionParticle;

    private void OnCollisionEnter(Collision collision)
    {
        else if (collision.gameObject.CompareTag("Obstacle"))
        {
            explosionParticle.Play();
        }
    }
}
```

#### 添加污垢飞溅颗粒

我们需要的下一个粒子效果是一个泥土飞溅，让玩家看起来像是踢地面，因为他们冲刺通过场景。

诀窍在于，粒子只应该在玩家在地面上的时候才 play。

1. Drag `FX_DirtSplatter` as the Player’s `child object`, reposition it, rotate it, and edit its settings
   1. rotation.z = -90
2. Declare a new `public ParticleSystem dirtParticle`;, then `assign` it in the Inspector
3. Add `dirtParticle.Stop()`; when the player jumps or collides with an obstacle
4. Add `dirtParticle.Play()`; when the player lands on the ground

```cs
public class PlayerController : MonoBehaviour
{
    public ParticleSystem dirtParticle;

    // Update is called once per frame
    void Update()
    {
        // 检测是否按下空格键
        if (Input.GetKeyDown(KeyCode.Space) && isOnGround && !gameOver)
        {
            dirtParticle.Stop();
        }
    }

    private void OnCollisionEnter(Collision collision)
    {
        if (collision.gameObject.CompareTag("Ground"))
        {            
            dirtParticle.Play();
        }
        else if (collision.gameObject.CompareTag("Obstacle"))
        {

            dirtParticle.Stop();
        }
    }
}
```

#### 向相机对象添加音乐
我们的粒子效果看起来很好，所以是时候转移到声音了！为了添加音乐，我们需要在相机上附加声音组件。毕竟，相机是场景的眼睛和耳朵。

1. Select the `Main Camera` object, then `Add Component > Audio Source`
2. From `Course Library > Sound`, drag a music clip onto the `AudioClip` variable in the inspector
3. Reduce the `volume` so it will be easier to hear `sound effects`
   1. Inspector -> Audio Source -> Volume
4. Check the `Loop` checkbox
   1. Inspector -> Audio Source -> Loop

#### 向 Player 添加音效

1. In `PlayerController.cs`, declare a new `public AudioClip jumpSound`; and a new `public AudioClip crashSound`;
2. From `Course Library > Sound`, drag a clip onto each new `sound` variable in the inspector
3. Add an `Audio Source` component to the `player`
4. Declare a new `private AudioSource playerAudio`; and initialize it as `playerAudio = GetComponent<AudioSource>();`
5. Call `playerAudio.PlayOneShot(jumpSound, 1.0f)`; when the character `jumps`
6. Call `playerAudio.PlayOneShot(crashSound, 1.0f)`; when the character `crashes`

```cs
public class PlayerController : MonoBehaviour
{
    public AudioClip jumpSound; // 用于存储跳跃音效的变量
    public AudioClip crashSound; // 用于存储碰撞音效的变量
    private AudioSource playerAudio; // 用于播放音效的音频源

    // Start is called before the first frame update
    void Start()
    {
        playerAudio = GetComponent<AudioSource>(); // 获取当前游戏对象上的 AudioSource 组件
    }

    // Update is called once per frame
    void Update()
    {
        // 检测是否按下空格键，并且玩家处于地面上且游戏未结束
        if (Input.GetKeyDown(KeyCode.Space) && isOnGround && !gameOver)
        {      
            playerAudio.PlayOneShot(jumpSound, 1.0f); // 播放跳跃音效
        }
    }

    // 当游戏对象碰撞到其他物体时调用
    private void OnCollisionEnter(Collision collision)
    {
        // 如果碰撞的物体标签为 "Ground"，则不做任何操作
        if (collision.gameObject.CompareTag("Ground"))
        {
            // Do nothing
        }
        // 如果碰撞的物体标签为 "Obstacle"，播放碰撞音效
        else if (collision.gameObject.CompareTag("Obstacle"))
        {           
            playerAudio.PlayOneShot(crashSound, 1.0f);
        }
    }
}
```

```cs
/// <summary>
///   <para>Plays an AudioClip, and scales the AudioSource volume by volumeScale.</para>
/// </summary>
/// <param name="clip">The clip being played.</param>
/// <param name="volumeScale">The scale of the volume (0-1).</param>
public void PlayOneShot(AudioClip clip, [UnityEngine.Internal.DefaultValue("1.0F")] float volumeScale)
{
    if ((Object) clip == (Object) null)
    Debug.LogWarning((object) "PlayOneShot was called with a null AudioClip.");
    else
    AudioSource.PlayOneShotHelper(this, clip, volumeScale);
}
```

> todo: 除开脚本调节音量，是否存在其他方式（声明puc var？）


### CWC 2 Challenge 3 - Balloons, Bombs, & Booleans


```cs
public class PlayerControllerX : MonoBehaviour
{
    public bool gameOver;

    public float floatForce;
    private float gravityModifier = 1.5f;
    private Rigidbody playerRb;

    public ParticleSystem explosionParticle;
    public ParticleSystem fireworksParticle;

    private AudioSource playerAudio;
    public AudioClip moneySound;
    public AudioClip explodeSound;


    // Start is called before the first frame update
    void Start()
    {
        // 3.The player can’t control the balloon
        playerRb = GetComponent<Rigidbody>();
        
        Physics.gravity *= gravityModifier;
        playerAudio = GetComponent<AudioSource>();

        // Apply a small upward force at the start of the game
        playerRb.AddForce(Vector3.up * 5, ForceMode.Impulse);

    }

    // Update is called once per frame
    void Update()
    {
        // While space is pressed and player is low enough, float up
        if (Input.GetKey(KeyCode.Space) && !gameOver)
        {
            playerRb.AddForce(Vector3.up * floatForce);
        }
    }

    private void OnCollisionEnter(Collision other)
    {
        // if player collides with bomb, explode and set gameOver to true
        if (other.gameObject.CompareTag("Bomb"))
        {
            explosionParticle.Play();
            playerAudio.PlayOneShot(explodeSound, 1.0f);
            gameOver = true;
            Debug.Log("Game Over!");
            Destroy(other.gameObject);
        } 

        // if player collides with money, fireworks
        else if (other.gameObject.CompareTag("Money"))
        {
            fireworksParticle.Play();
            playerAudio.PlayOneShot(moneySound, 1.0f);
            Destroy(other.gameObject);

        }

        // 9.Bonus: The balloon can drop below the ground
        else if (other.gameObject.CompareTag("Ground"))
        {
            playerRb.AddForce(Vector3.up * 15, ForceMode.Impulse);
        }

    }

}
```

```cs
public class MoveLeftX : MonoBehaviour
{
    public float speed;
    private PlayerControllerX playerControllerScript;
    private float leftBound = -10;

    // Start is called before the first frame update
    void Start()
    {
        playerControllerScript = GameObject.Find("Player").GetComponent<PlayerControllerX>();
    }

    // Update is called once per frame
    void Update()
    {
        // If game is not over, move to the left
        // 4.The background only moves when the game is over
        if (!playerControllerScript.gameOver)
        {
            transform.Translate(Vector3.left * speed * Time.deltaTime, Space.World);
        }

        // If object goes off screen that is NOT the background, destroy it
        if (transform.position.x < leftBound && !gameObject.CompareTag("Background"))
        {
            Destroy(gameObject);
        }

    }
}
```

```cs
public class SpawnManagerX : MonoBehaviour
{
    public GameObject[] objectPrefabs;
    private float spawnDelay = 2;
    private float spawnInterval = 1.5f;

    private PlayerControllerX playerControllerScript;

    // Start is called before the first frame update
    void Start()
    {
        // No objects are being spawned
        InvokeRepeating("SpawnObjects", spawnDelay, spawnInterval);
        playerControllerScript = GameObject.Find("Player").GetComponent<PlayerControllerX>();
    }

    // Spawn obstacles
    void SpawnObjects ()
    {
        // Set random spawn location and random object index
        Vector3 spawnLocation = new Vector3(30, Random.Range(5, 15), 0);
        int index = Random.Range(0, objectPrefabs.Length);

        // If game is still active, spawn new object
        if (!playerControllerScript.gameOver)
        {
            Instantiate(objectPrefabs[index], spawnLocation, objectPrefabs[index].transform.rotation);
        }

    }
}

```

```cs
public class RepeatBackgroundX : MonoBehaviour
{
    private Vector3 startPos;
    private float repeatWidth;

    private void Start()
    {
        startPos = transform.position; // Establish the default starting position 
        // 7.The background is not repeating properly
        repeatWidth = GetComponent<BoxCollider>().size.x / 2; // Set repeat width to half of the background
    }

    private void Update()
    {
        // If background moves left by its repeat width, move it back to start position
        if (transform.position.x < startPos.x - repeatWidth)
        {
            transform.position = startPos;
        }
    }
}
```

### CWC 2 Lab 3 - Player Control

#### 3.Constrain the Player’s movement
1. 如果你的玩家正在与不应该碰撞的物体（包括地面）碰撞，请在碰撞器组件中 check `Is trigger` box
2. 如果玩家的位置或旋转应该受到约束，则扩展刚体组件中的 `constraints` 并约束某些轴
3. 如果你的玩家可以离开屏幕，写一个if语句检查和重置位置
4. 如果玩家可以 double-jump 或飞离屏幕，创建一个布尔变量来限制用户的能力
5. 如果你的玩家应该受到游戏区域外部的物理障碍的限制，创建更原始的平面或立方体，并将它们缩放成墙壁



### CWC 2 Unit 4 - Gameplay Mechanics


#### 3.Create a focal point for the camera

1. Create a new Empty Object and rename it `Focal Point`, 
2. `Reset its position` to the origin (0, 0, 0), and make the Camera a `child object` of it
3. Create a new “Scripts” folder, and a new `RotateCamera` script inside it 
4. Attach the `RotateCamera` script to the Focal Point

#### 4.Rotate the focal point by user input

1. Create the code to rotate the camera based on `rotationSpeed` and `horizontalInput`
2. Tweak the rotation speed value to get the speed you want

```cs
public class RotateCamera : MonoBehaviour
{
    public float rotationSpeed;
    
    // Start is called before the first frame update
    void Start()
    {
    }

    // Update is called once per frame
    void Update()
    {
        float horizontalInput = Input.GetAxis("Horizontal");
        transform.Rotate(Vector3.up, horizontalInput * rotationSpeed * Time.deltaTime);
    }
}
```

#### 5.Add forward force to the player

1. Create a new `“PlayerController”` script, apply it to the Player, and open it
2. Declare a new `public float speed variable` and `initialize` it
3. Declare a new `private Rigidbody playerRb` and `initialize it in Start()`
4. In `Update()`, declare a new `forwardInput` variable based on `“Vertical”` input 
5. Call the `AddForce()` method to move the player forward based forwardInput

```cs
public class PlayerController : MonoBehaviour
{
    private Rigidbody playerRb;
    public float speed = 5.0f;

    void Start()
    {
        playerRb = GetComponent<Rigidbody>();
    }

    // Update is called once per frame
    void Update()
    {
        float fowardInput = Input.GetAxis("Vertical");
    }
}
```

#### 6.Move in direction of focal point

1. Declare a new `private GameObject focalPoint`; and initialize it in `Start()`: `focalPoint = GameObject.Find("Focal Point");`
2. In the `AddForce` call, Replace` Vector3.forward` with `focalPoint.transform.forward`

```cs
public class PlayerController : MonoBehaviour
{
    private GameObject focalPoint;
    
    void Start()
    {
        focalPoint = GameObject.Find("Focal Point");
    }

    // Update is called once per frame
    void Update()
    {
        playerRb.AddForce(focalPoint.transform.forward * (speed * fowardInput));
    }
}
```

> 可选：花点时间来尝试一下 `Global` 与 `Local` 切换菜单，看看两者之间的切换如何改变坐标和定位。

![image](https://unity-connect-prd.storage.googleapis.com/20231214/learn/images/08f436eb-b052-4623-a97d-1e2f4da5a364_image.png)


## Unity Essentials

#### Render mode
在Unity中设置Canvas的Render Mode可以通过以下步骤完成：

在Unity编辑器中打开Canvas对象。
在Inspector面板中，找到Canvas组件。
在Canvas组件下的Render Mode属性中，你可以选择不同的渲染模式。常见的选项包括：
Screen Space - Overlay：Canvas将覆盖在场景中的所有其他对象之上，不会随着场景中的相机移动而移动。
Screen Space - Camera：Canvas将放置在场景中的一个特定相机的前面，你需要指定一个目标相机。
World Space：Canvas将以世界坐标的形式存在，可以在场景中移动和旋转，通常用于在3D场景中创建HUD或者3DUI。

> [Unity certificate](https://unity.com/cn/products/unity-certifications/user-programmer)

#### Scene操作

1. 按住` 右键 + WASD` 可以以游戏视角调整视角
2. F键聚焦
3. 使用滚轮进行放大和缩小，按住滚轮进行平移
4. 选中对象后，按住` option + 左键` 单击可绕焦点旋转，或按住 `Option + 右键` 单击可放大和缩小


#### Camera Projection
在camera的inspector里调整。

1. 透视投影（Perspective）：

- 透视投影模拟了人眼在现实世界中的视觉效果。远处的物体看起来比较小，而近处的物体看起来比较大，同时也存在景深（近大远小）效果。
- 透视投影会根据摄像机和物体之间的距离产生景深效果，远离摄像机的物体将显示得比较小，而靠近摄像机的物体将显示得比较大。

2. 正交投影（Orthographic）：

- 正交投影消除了景深效果，使得物体在屏幕上显示的大小与其距离摄像机的距离无关。无论物体距离摄像机多远，它们在屏幕上的大小都是固定的。
- 正交投影在一些2D游戏或需要简化透视效果的情况下很有用，例如俯视视角的游戏、UI界面等。
- 用size调整取景范围
  
如果你想要实现更加现实的视觉效果，或者需要在游戏中表现景深效果，则使用透视投影是一个不错的选择。
如果你的游戏是2D游戏，或者你想要简化透视效果并让物体在屏幕上的大小保持固定，那么使用正交投影可能更合适。


#### LateUpdate() 和 Update()

Update方法：

- Update方法在每一帧渲染之前被调用，因此它用于处理对象的常规更新逻辑，例如移动、用户输入响应等。
- 由于它在每一帧渲染之前执行，所以它是处理大多数游戏对象行为的理想位置。

LateUpdate方法：

- LateUpdate方法在所有Update方法执行完毕后被调用，所以它通常用于处理在Update方法中进行了一些更改后的后续调整或校正。
    例如，如果在Update方法中移动了一个对象，并且希望另一个对象跟随该对象移动，那么可以将跟随逻辑放在LateUpdate方法中，以确保它们在位置调整之后执行。
- LateUpdate还经常用于处理摄像机相关的逻辑，因为它能确保所有其他对象都已经更新完毕，摄像机再进行调整，从而避免画面抖动等问题。

#### 玩家控制输入

1. Explore the inputs: click `Edit` > `Project Settings`, select `Input Manager` in the left sidebar, then expand the `Axes` fold-out to explore the inputs

```cs
        if (Input.GetKeyDown(KeyCode.Space)) {
            // Launch a projectile from the player
            Instantiate(projectilePrefab, transform.position, projectilePrefab.transform.rotation);
        }

        // In order to improve game performance, we need to destroy them when they go out of bounds.
        if (transform.position.z > topBound) {
            Destroy(gameObject);
        }
        // 如果是要应用到全部prefab的clone，在inspector =》 override => apply all
```

- animalPrefabs[animalIndex]表示将要实例化的游戏对象的预制体。animalPrefabs是一个数组或列表，存储了多个预制体。animalIndex是一个整数变量，用于指定要实例化的预制体在数组中的索引。
- new Vector3(0, 0, 20)表示实例化后游戏对象的初始位置。这里的代码将在世界坐标系中创建一个新的位置，x和y坐标为0，z坐标为20。
- animalPrefabs[animalIndex].transform.rotation表示实例化后游戏对象的初始旋转。这里的代码获取了将要实例化的预制体的旋转信息，并将其应用于新创建的游戏对象。

```cs       
        if (Input.GetKeyDown(KeyCode.S))
        {
            Instantiate(
                animalPrefabs[animalIndex], 
                new Vector3(0, 0, 20), 
                animalPrefabs[animalIndex].transform.rotation
                );
        }        

```

#### 边界限制
```cs
        if (Mathf.Abs(transform.position.z) <= bound)
        {
            transform.Translate(Vector3.right * moveSpeed * Time.deltaTime * verticalInput);
        }
        else
        {
            transform.position = new Vector3(transform.position.x, transform.position.y, transform.position.z > 0 ? bound : -bound);
        }
```

# Handbook
## 2D 项目
#### Layer
Inspector => order in layer

#### Pos固定
RigidBody 2D => Dynamic => constraints freeze

或者

RigidBody 2D => Static


# 项目及团队

## 流程

#### 游戏设计文档
包括有关故事、游戏玩法、艺术指导、预期目标受众和可访问性的信息。

#### 生产

![分工图](https://unity-connect-prd.storage.googleapis.com/20200923/learn/images/00c0dbf7-09fe-49b8-858a-a75e55c1eddd_Foundations_UnityRT3D_1.1.3.2_chart_of_jobs.png)

#### 后期制作
评估、编辑、润色和修复。这通常包括alpha 测试和beta 测试。 

Alpha 测试是在内部进行的，以确定问题和需要改进的领域，而 Beta 测试是由潜在的最终用户在产品使用的预期环境中进行的。

#### GDD
设计文档包含您的项目的蓝图，包括：
- 高层概述；例如，游戏（或体验）设计文档中的总体项目愿景
- 项目中特定管道的要求和标准
- 特定功能的详细设计规范

您应该确定：
- 该项目的目标和目的
- 目标用户和受众
- 该项目的主要特点
- 最终交付形式

[GDD Sample](https://docs.google.com/document/d/1o1KFkuZrPbevpd7ZYBhJ5e8n3GRg6m15HkebVfiTufk/edit)

#### 项目管理
[Agile风格的项目管理文件 Sample](https://docs.google.com/document/d/1FR-GYr2hL67d6MleWTTP-mXfCHVZTM1Mko77MFodxFg/copy)

#### 项目章程 Project Charter
设计文件获得批准并且项目被批准生产，项目章程就很有用，特别是当您在团队中工作时。

这是一份正式文件，描述了整个项目，包括项目的目标、项目的实施方式以及利益相关者是谁。项目章程用于预生产和生产阶段。

项目章程通常包括：
- 项目理由
- 项目的目标和限制
- 主要利益相关者是谁
- 已识别的风险
- 项目效益
- 预算总体概述

[Project Charter Sample](https://docs.google.com/document/d/1CzqyP1Qn8Ag-lXPaWVynb0InxUkXyWZLnkY2RllUSj8/edit)

#### 管理项目，项目跟踪器
通过规划适当的时间表和管理项目计划来管理项目

项目计划采用设计文件和项目章程中确定的要素，并设置具体任务和交付日期。制作人或项目经理通常会创建此计划，并在需要进行更改时根据需要进行更新。

针对`个人和团队成功跟踪项目`的一些指南包括：
- 确定必要的项目步骤。
- 如果在团队中工作，请确定并分配特定的项目角色和职责。
- 创建包含具体可交付成果和截止日期的时间表。
- 识别项目管理中的常见问题和问题，例如范围蔓延和过于雄心勃勃的设计计划以及紧迫的时间限制。
- 确定已完成项目的到期时间。
- 为将构建到整个项目的项目的每个较小部分设置截止日期。
- 为每个项目阶段制定合理的时间框架。
- 如果在团队中工作，请为列表中的每项任务指定任务所有者。


### 测试

#### 错误报告的艺术
[错误报告的艺术](https://www.ministryoftesting.com/articles/the-art-of-the-bug-report)


### 运营

#### 项目回顾
进行回顾的一种简单方法是制作一个包含三列的图表，并确定您认为应该做的事情：
- 开始做
- 不要做了
- 继续做



# DCC

#### 3D 资源获取

ProBuilder: 在 Unity 编辑器中创建 3D 艺术和环境。与专用 DCC 相比，Probuilder 的功能有限，但对于想要在不打开外部编辑工具的情况下快速建模 3D 对象的艺术家来说，它很有帮助。  

在线资源: CGTrader, Turbosquid 3D，Unity Asset Store也是专为 Unity 设计的宝贵艺术资源。

#### 2D 资源
Unity 具有专门为处理 2D 资源而设计的内置工具。例如，`2D Tilemap Editor` 可帮助快速设计 2D 关卡，
而`Sprite Editor`则可管理进入 2D 动画的各种图像（“Sprite”）。有专门用于2D 物理、2D 灯光等的系统。


#### 音频资源获取
音频数字创作工具 (DCC)，例如Audition、Logic Pro、Reaper和Audacity


### Audio
##### 3D 音效
Audio source => spatial blend
https://learn.unity.com/tutorial/create-real-time-3d-audio-effects?uv=2021.3&pathwayId=5f7bcab4edbc2a0023e9c38f&missionId=5f777d9bedbc2a001f6f5ec7&projectId=5faab859edbc2a00209536ce#