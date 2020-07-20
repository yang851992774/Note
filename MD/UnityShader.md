# 渲染流水线

**应用阶段：**

- 把数据加载到显存
- 设置渲染状态（Vetex Shader/Fragment Shader  光源属性，材质等）
- 调用Draw Call

**几何阶段**：

当GPU从CPU那里得到渲染命令后，就会进行一系列流水线操作，最终把图元渲染到屏幕上。

- 顶点着色器（MVP）(完全可编程)
- 裁剪（可配置）
- 屏幕映射（完全不可编程，不可配置）

**光栅化阶段**：

- 三角形设置  - 得到整个三角网格对像素的覆盖情况
- 三角形遍历 - 检查每个像素是否被一个三角网格所覆盖（生成片元）
- 片元着色器 - 纹理采样，对三角网格的3个顶点对应的纹理坐标进行插值
- 逐片元操作 - （输出合并）片元-> 模板测试-> 深度测试 ->混合 ->颜色缓冲区



# 光照模型

**标准光照模型**

**Phong光照模型  / Blinn-Phong光照模型**

漫反射：diffuse * (max(0,dot(n,l)))                     n 法线   l 入射光线

高光:       specular * pow( max(v,r) ,gloss)          v 视觉方向   ， r 发射方向  gloss 光泽度

Blinn高光 ：specular * pow( max(n,h) ,gloss)   n 法线    h=(v+l)/(|v+l|) 视觉方向和入射光的中心角度的单位向量

**半兰伯特光照模型** 解决不在光照的面全黑的问题

漫反射：diffuse * (0.5*max(0,dot(n,l)) + 0.5)       n 法线   l 入射光线



**BRDF光照模型**

**PBR光照模型**



# 基础纹理

法线纹理

渐变纹理

遮罩纹理



# 透明效果

**渲染规则：**

先渲染不透明物体，然后渲染不透明物体，不透明物体需要从后往前渲染。

**透明测试-溶解**

**透明混合**

Blend Off

Blend SrcFactor  DetFactor

Blend SrcFactor  DetFactor  SrcFactorA  DetFactorA

**复杂模型的透明物体（我们无法对模型进行像数级别的深度排序）**

开启深度写入的半透明   -  使用2个Pass 

第一个Pass :开启深度入，但不进行颜色输出   ColorMask RGB | A | 0

第二个Pass :由于上个Pass 已经开启了深度写入，所有可以按照像数深度排序，进行透明渲染。（增加一个Pass 造成性能问题）

**双面渲染的透明效果**

在两个Pass 中分别剔除不同的朝向



# 更加复杂的光照

**Unity渲染路径**   LightMode

| 标签         | 描述                                                        |
| ------------ | ----------------------------------------------------------- |
| Always       |                                                             |
| ForwordBase  | 会计算环境光，重要的平行光，逐顶点光照/SH光源和LightMaps    |
| ForwordAdd   | 会计算额外的逐像数光源，每个Pass 对应一个光源               |
| ShadowCaster | 把物体深度信息渲染到阴影纹理（Shadowmap）或者一张深度纹理中 |
| Defered      | 延迟，该Pass会渲染到G缓冲                                   |
|              |                                                             |

**光照衰减**

_LightTexture0  _LightMatrix

float3 lightCoord = mul(_LightMatrix0,float4(i.worldPosition,1)).xyz;

fixed atten = tex2D(_LightTexture0,dot(lightCoord,lightCoord).rr).UNITY_ATTEN_CHANNEL;

使用光源空间中顶点距离平方，对光照衰减纹理采样，UNITY_ATTEN_CHANNEL来得到衰减纹理中衰减值所在的分量



**阴影实现原理**

Shadow Map 技术，先将摄像机的位置放置与光源重合的位置，场景中该光源阴影区域就是相机看不到的地方，

如果场中重要光源开启阴影，Unity就会为该光源计算它的阴影纹理（shadowmap）。这张阴影纹理本质上是一张深度图。记录着该光源的位置出发、能看到的场景中距离它最近的表面位置（深度信息）

**不透明物体阴影**

SHADOW_COORDS            声明一个可用的插值寄存器

TRANSFER_SHADOW         计算阴影纹理坐标

SHADOW_ATTENUATION    计算阴影值

**透明物体阴影**

**高级纹理**



**折射  涅菲尔**

站在湖边，直接看脚边的水面时，你会发现水几乎是透明的。可以看到水下的小鱼和石头。

抬头看远方湖面，会发现几乎看不到水下的情景，只看到反射环境。

涅菲尔近视等式

Fschlick = F0 + （1-F0）(1-n.v)^5

Fschlick = F0 + （1-F0）(1-n.v)^5

从公式上可以看出，当法线方向和视角方向很小时候（近处看物体），Fschlick  ≈ F0,几乎全是折射

当法线方向和视角方向很大（远处看物体），Fschlick  ≈ F0 + （1-F0） ≈ = 1,几乎全是反射。

resultColor =  lerp(diffuse,reflection,fresnel)



**渲染纹理   VS  GrabPass** 

GrabPass  - 抓取屏幕



**程序纹理**





# 动画

**纹理动画**

**顶点动画**   DisableBatching   顶点动画阴影注意

**广告牌**





**屏幕后期处理**

**亮度**   Text.rgb  * _Bringhtness

**饱和度**   luminance = 0.2125 * Text.r + 0.7154 * Text.g  + 0.0721 * Text.b

​              luminanceColr = fixed3(luminance ,luminance ,luminance );

​			 lerp(luminanceColr ,finalColor,_Saturation)

**对比度**

​			avgColor = flxed3(0.5,0.5,0.5);

​			lerp(avgColor,finalColor,_Contrast)





**边缘检测**

卷积   边缘检测算子

​			![image-20200611121532324](G:\新建文件夹\MD\MD插图\image-20200611121532324.png)	

**模糊**

卷积    高斯模糊，正太分布，权重为1  

![image-20200611121753857](G:\新建文件夹\MD\MD插图\image-20200611121753857.png)





**Bloom 效果**

 通过一个阀值提取出图像较高亮区域，把他存储到一个渲染纹理中，再利用高斯模糊对这张纹理进行模糊处理，模拟光线扩散的效果。最终和原图进行混合。





**运动模糊**





# 使用深度和发现纹理



# 非真实渲染



# 使用噪声

消融效果

水波效果

# Unity渲染优化技术



# 表面着色器



# 基于物理的渲染





**Shder优化**



CPU 端软件裁剪是否高效正确？‘

overdraw 是否有效避免？

远处的阴影是否真的需要开启？

renderTarget 是否可以小一点？

常用的后期处理是否可以合成一次做完？



保证效果的前提下，将计算放在顶点着色器处理

多pass 会打断合批

使用LOD ,MipMap 、Mesh Lod 、Shader Lod

gup执行f两个float 乘法和 两个vector效率是一样的

少用分支，大多数条件分支可以用数值方式替换 step

多使用内置函数，而不是自行实现

fixed half  float 在不同设备性能不同

避免复杂运算，sqrt 三角函数等



shader变体优化 