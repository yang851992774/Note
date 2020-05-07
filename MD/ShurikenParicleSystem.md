

# 粒子系统

## 一、粒子系统基本属性

| 属性               | 类型    | 描述                                                         |
| ------------------ | ------- | ------------------------------------------------------------ |
| During             | number  | 粒子系统发射总时长                                           |
| Looping            | boolean | 是否循环                                                     |
| Prewarm            | boolean | 是否预热，预热会把所有粒子全部准备好，Play那一刻就会有很多粒子 |
| Start Delay        | number  | 粒子系统发射延迟                                             |
| Start LifeTime     | number  | 单个粒子的生命时长                                           |
| Start Speed        | number  | 粒子开始速度，默认是朝+Z 方向发射，所有一般为了向上发射，需要把粒子系统绕x轴旋转-90、还影响Shape中的高度，速度大了、高度肯定也会增大 |
| 3D Start Size      | Vector3 | 单个粒子不同方向的初始大小                                   |
| Start Size         | number  | 单个粒子整体大小                                             |
| Start Rotation     | number  | 单个粒子旋转                                                 |
| 3D Start Rotation  | Vector3 | 单个粒子初始旋转                                             |
| Randomize Rotation | number  | 单个粒子随机选择  0~1                                        |
| Start Color        | Color   | 粒子颜色 透明度                                              |
| Gravity Modifier   | number  | 重力                                                         |
| Simulation Space   | enum    | 发射空间（Local 粒子在局部空间游荡/World 粒子在世界空间游荡 /Custom） |
| Simulation Speed   | number  | 发射速度，    Start Speed * Simulation Speed                 |
| Delta Time         | enum    | Scaled/UnScaled  发射速度受时间缩放影响                      |
| Scaling Mode       | enum    | 影响大小模式  Hierarchy受父节点和自身双重影响/Local子受子节点/Shape只是发射范围变大，自身大小不受不受父节点和自身节点改变，影响Shape 的大小 |
| Play On Awake      | boolean | 游戏运行是否自动播放                                         |
| Emitter Velocity   | enum    | 发射速度受什么影响 Transform/Rigibody                        |
| Max Particles      | number  | 最大发射粒子数量                                             |
| Auto Random Seed   | boolean | 每次设置随机数，重置随机种子                                 |
| Stop Action        |         |                                                              |
| Culling Mode       |         |                                                              |
| Ring Buffer Mode   |         |                                                              |
|                    |         |                                                              |

## 二、粒子系统模块

- ## 1、Emission   发射模块

  | 属性               | 类型         | 描述                           |
  | ------------------ | ------------ | ------------------------------ |
  | Rate over Time     | number       | 每秒发射粒子数量               |
  | Rate over Distance | number       |                                |
  | Bursts             | List<Struct> | 参照下面结构体，时间轴控制爆发 |
  | Bursts-Time        | number       | 时间轴 < During                |
  | Bursts-Min         | number       | 爆发发射最小个数粒子           |
  | Bursts-Max         | number       | 爆发发射最大个数粒子           |
  | Bursts-Cycle       | number       | 爆发发射次数                   |
  | Bursts-Interval    | number       | 爆发发射间隔                   |
  | Bursts-Probability | number       | 爆发发射概率                   |

  

- ## 2、Shape   发射形状范围

  | 属性                | 类型    | 描述                                                         |
  | ------------------- | ------- | ------------------------------------------------------------ |
  | Shape               | enum    | 发射形状范围                                                 |
  | Thickness           | number  | 厚度 0 ~1                                                    |
  | Arc                 | number  | 发射角度范围0~360                                            |
  | Arc.Mode            | enum    | Random/Loop/Ping Pang/Burst Speed                            |
  | Arc.Speed           | number  |                                                              |
  | Emit from           | enum    | Base 只会从底座产生粒子/ Volume随机从 容器体积内产生粒子  （不同形状表含义不一样） |
  | Position            | Vector3 | 局部位置                                                     |
  | Rotation            | Vector3 | 局部旋转                                                     |
  | Scale               | Vector3 | 局部大小                                                     |
  | Align To Direction  | boolean | true 粒子平面 发射方向保持垂直，从其他方向会看是扁平的，false 正常效果 |
  | Randomize Direction | number  | 随机方向0~1                                                  |
  | Spherize Direction  | number  | 球形方向0~1                                                  |
  | Randomize Position  | number  | 随机位置范围0~正无穷                                         |
  |                     |         |                                                              |

  Shape 3D形状 :[ Spere  球体内随机发射、HemiSphere 、Cone、Dount 圆形跑道、Box、Mesh、Meshrender、SkinnedMeshRender ]

  Shape 2D形状  [ Sprite、SpriteRender、Circle、Edge、Rectangle]

- ## 3、Velocity over Lifetime  控制粒子生命周期内速度变化

|        |                                        |                   |
| ------ | -------------------------------------- | ----------------- |
| Linear | Constant /Curve/Rnd2Constant/Rnd2Curve | (Vector3/Curver/) |
|        |                                        |                   |
|        |                                        |                   |
|        |                                        |                   |



- ## 4、Inherit Velocity

- ## 5、Force over Lifetime

- ## 6、Color over Lifetime   粒子在生命周期颜色和透明度变化

  要新增颜色和透明度直接在颜色面板点击就会新增一个节点、要删除一个颜色和透明节点直接点击往外拖拽移除

  |       |       |                      |
  | ----- | ----- | -------------------- |
  | Color | color | 颜色和透明度变化曲线 |
  | Blend | enum  | 混合模式             |
  |       |       |                      |

  

- ## 7、Color by Speed

- ## 8、Size over Lifetime

- ## 9、Size by Speed

- ## 10、Rotation over Lifetime

- ## 11、Rotation by Speed

- ## 12、External Forces

- ## 13、Noise

- ## 14、Collision  粒子特效的碰撞

|                         |         |                                                              |
| ----------------------- | ------- | ------------------------------------------------------------ |
| Dampen                  | number  | 抑制（0~1），选这个为1时（完全抑制），碰撞之后，阻止了粒子，可以使碰撞的粒子消失 |
| Bounce                  | number  | 反弹（0~2），选完这个之后，可以让产生碰撞的粒子以某个角度反弹出去 |
| Lifetime Loss           | number  | 生命周期损失（0~1），碰撞之后让粒子损失百分比的生命周期，为1时（生命周期完全损失），可以使粒子消失 |
| Min Kill Speed          | number  | 最小清除速度，设置值越大，粒子发生碰撞之后被移除的速度越快，当达到某个值之后，可以近似碰撞之后立即消失 |
| Max Kill Speed          |         |                                                              |
| Send Collision Messages | boolean | void OnParticleCollision(GameObject other)  true 的话，碰撞体对象会接收到这个方法 |
| Collision Quality       | enum    | 碰撞质量，设置发生碰撞的碰撞概率大小，选项三项从上到下由高到低，越低碰撞到的概率就越低 |

可以使粒子消失的方法有以下三种

（1）设置Dampen为1；

（2）设置Lifetime Loss为1；

（3）设置较大的Min Kill Speed值

- ## 15、Triggers

- ## 16、Sub Emitters

- ## 17、Texture Sheet Animation

  序列帧动画

  | 属性                 | 类型    | 描述                                                         |
  | -------------------- | ------- | ------------------------------------------------------------ |
  | Tiles                | Vector2 | 序列帧平铺                                                   |
  | Mode                 | enum    | Grid/Sprites                                                 |
  | Animation            | enum    | WholeSheet （整体）/Single Row（单行：表单的每一行代表一个单独的动画序列） |
  | Time Mode            | eunm    | Lifetime/Speed/Fps                                           |
  | StartFrame           | number  | 允许您指定粒子动画应该在哪个帧上开始（对每个粒子随机调整动画有用） |
  | Cycles               | number  | 动画序列在粒子寿命期间重复的次数。                           |
  | Affected UV Channels | enum    | 特效UV管道 Everying/Nothing/UVn                              |
  | Frame over Time      |         | 指定动画框架随着时间的推移而增加的曲线。                     |

  

- ## 18、Lights

- ## 19、Trails

- ## 20、Custom Data

- ## 21、Renderer   单个粒子形状&表现模块

| 属性           | 类型 | 描述                                                         |
| -------------- | ---- | ------------------------------------------------------------ |
| Render Mode    | enum | BillBoard  面片/Stretched BillBoard 上下左右拉伸/Horizontal BillBoard 左右拉伸/Vertical Billboard 上下拉伸 /  Mesh 单个粒子自定义Mesh (可以增加多个网格) |
| Meterial       |      | Mode 使用的材质                                              |
| Trail Material |      | 拖尾材质                                                     |
|                |      |                                                              |
|                |      |                                                              |
|                |      |                                                              |
|                |      |                                                              |
|                |      |                                                              |
|                |      |                                                              |
|                |      |                                                              |
|                |      |                                                              |
|                |      |                                                              |
|                |      |                                                              |
|                |      |                                                              |



edge     n. 边缘；优势；刀刃；锋利

thickness   n. 厚度；层；浓度；含混不清

## 



