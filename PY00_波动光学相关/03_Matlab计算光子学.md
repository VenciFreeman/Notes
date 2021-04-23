# Matlab_计算光子学

## 绪论

### 什么是光子学

- 涉及电磁能量的场

  - 光子学与涉及电子的电子学是平行的

  - 光子之间不相互作用

### 什么是计算光子学

- 利用数值方法研究光在波导结构中的特性和传播

- 利用分析和计算模型来研究光的行为和光与物质的相互作用

- 方法：计算电磁学

  - 广义的三类问题

    - 频域特征计算

    - 频域解算

    - 时域模拟

  - CAD建模中使用的主要算法 (没有普适性)

    - 波束传播法 (BPM)

    - 本征模式展开法 (EME)

    - 时域有限差分法 (FDTD)

  - 考察指标

    - 速度

    - 存储利用率

    - 数值孔径

    - 折射率在器件中的对比

    - 极化、损耗、反射和非线性

### 应用

- 计算纳米光子学

  - 在这种尺度下，多重散射和近场效应对光的传播和光物相互作用有较大的影响

  - 最终的目标是创造出三维光子结构

    - 可能会引发渐进式光学计算

    - 有朝一日可能实现全光学计算

- 光纤通信 (略)

- 生物和医学光子学 (略)

- 光子传感器 (略)

- 硅光子学
  - 硅不是直接间隙材料，因此不能有效地产生光

- 光量子信息科学 (略)

## 光学基本知识

### 几何光学

- 概述

  - 几何光学是以射线的概念为基础的

  - 射线是光学效果的几何表征

- 射线理论及其应用

  - 斯涅耳定律：平面界面处，透射射线的方向

  - 菲涅耳公式：平面波导中两种主要类型的波的反射系数

- 关键角度

  - 临界角θ满足
    $$
    sinθ=\frac{n_2}{n_1}
    $$
    

- 棱镜
  
- 只关注薄透镜：可以忽略光线穿过透镜时的垂直平动
  
- GRIN系统

  - GRIN：折射率梯度 (GRadient in the INdex of refraction)

  - 材料折射率不均匀，有空间依赖性

  - 为了使光线聚集在焦点上，所有光线的光路必须相同

  - 光程：给定区域的几何距离与该区域的折射率的乘积

  - 为了使平行光通过GRIN圆盘聚焦，折射率应该以二次函数关系依赖于半径

### 波动光学

#### 概述

- 光作为电磁波，由电场矢量和垂直磁场矢量组成

- 以10^14Hz量级振荡并沿垂直电场矢量和磁场矢量的方向在空间中运动

- 电场矢量符合波动方程

  

  - 与时间无关，可由此建立斯托克斯关系

- 介质中一维波动方程

$$
\frac{1}{v^2}\frac{\part^2}{\part t^2}E(z,t)=\frac{\part^2}{\part z^2}E(z,t)
$$



#### 相速度

- 选择一个点，假设这一点保持恒定相

- $v_p=\frac{dz}{dt}=ω/k$

- 代表恒定相面在介质中移动的速度

#### 群速度

- 脉冲在介质中的传播速度
  $$
  E(z,t)=2E_0 cos(kz-\omega t)cos(\Delta kz-\Delta\omega t)
  $$

- 表示载波频率为$~\omega~$的波被拍频$~\Delta\omega~$的正弦包络所调制

$$
v_g=\frac{\Delta\omega}{\Delta k}\rightarrow \frac{d\omega}{dk}
$$

- 在自由空间 (真空)中，相速度和群速度是相同的

#### 斯托克斯关系

- 描述光在两介质界面面上的反射率和透射率
- 光以任意角度$~θ_i~$入射时单片薄膜中的干涉

![用于导出斯托克斯关系的界面传输和反射的完整过程](../fig/PY00/PY00_chapter03_fig01.jpg)
$$
r^2E+t'tE=E\\
rtE+r'tE=0
$$
由此得到斯托克斯关系
$$
t't=1-r^2\\
r'=-r
$$

#### 介质膜干涉

- 通过计算光程差推导建设性干涉和破坏性干涉的条件
- 光穿过薄膜所获得的相位差$\delta$与光程差$\Delta$对应关系为

$$
\delta=k\cdot\Delta=\frac{2\pi}{\lambda_0}\cdot\Delta
$$

#### 平行板中的多重干涉

- 辐照度$~I_R~$

$$
I_R=\frac{2r^2(1-cos\delta)}{1+r^4-2r^2cos\delta}I_i
$$

$$
I_T=\frac{(1-r^2)^2}{1+r^4-2r^2cos\delta}I_i
$$

有
$$
I_R+I_T=I_i
$$

### MATLAB

|      函数名      |            描述             |
| :--------------: | :-------------------------: |
| phase_velocity.m |         相速度绘图          |
| group_velocity.m |         群速度绘图          |
|  FP_transmit.m   | 法布里-珀罗标准具透射比绘图 |

#### 相速度绘图

```matlab
% File name: phase_velocity.m
% Illustrative plot of phase velocity
clear all
N_max = 101;  % number of points for plot
t = linspace(0,30d-15,N_max);  % creation of theta arguments
%
c = 3d14;  % velocity of light in microns/s
n = 3.4;  %  refractive index
v_p = c/n;  % phase velocity
lambda = 1.0;  % microns
k = 2*pi/lambda;
frequency = v_p/lambda;
z = 0.6;  % distance in microns
omega = 2*pi*frequency;
A = sin(k*z - omega*t);
plot(t,A,'LineWidth',1.5)
xlabel('Time','FontSize',14);
ylabel('Amplitude','FontSize',14);
set(gca,'FontSize',14);  % size of tick marks on both axes
axis([0 30d-15 -1.5 2])
text(17d-15, 1.3, 'z(t)','Fontsize',16)
line([1.53d-14,2d-14],[1,1],'LineWidth',3.0)  % drawing arrow
line([1.9d-14,2d-14],[1.1,1],'LineWidth',3.0)
line([1.9d-14,2d-14],[0.9,1],'LineWidth',3.0)
pause
close all
```

#### 群速度绘图

```matlab
% File name: group_velocity.m
% Illustrative plot of group velocity by superposition
% of two plane waves
clear all
N_max = 300;  % number of points for plot
t = linspace(0,300d-15,N_max);  % creation of theta arguments
%
c = 3d14;  % velocity of light in microns/s
n = 3.4;  % refractive index
v_p = c/n;  % phase velocity
lambda = 1.0;  % microns
frequency = v_p/lambda;
z = 0.6;  % distance in microns
omega = 2*pi*frequency;
k = 2*pi/lambda;
Delta_omega = omega/15.0;
Delta_k = k/15.0;
%
omega_1 = omega + Delta_omega;
omega_2 = omega - Delta_omega;
k_1 = k + Delta_k;
k_2 = k - Delta_k;
A = 2*cos(k*z - omega*t).*cos(Delta_k*z - Delta_omega*t);
plot(t,A,'LineWidth',1.3)
xlabel('Time','FontSize',14)
ylabel('Amplitude','FontSize',14)
set(gca,'FontSize',14);  % size of tick marks on both axes
pause
close all
```

#### 法布里-珀罗标准具透射比绘图

```matlab
% FP_transmit.m
% Plot of transmittance of FP etalon
clear all
N_max = 401;  % number of points for plot
t = linspace(0,1,N_max);  % creation of theta arguments
delta = (5*pi)*t;  % angles in radians
%
hold on
for r = [0.2 0.4 0.8]  % reflection coefficient
F = 4*r^2/(1-r^2).^2;  % coefficient of finesse
T = 1./(1 + F*(sin(delta/2)).^2);
plot(delta,T,'LineWidth',1.5)
end
%
% Redefine figure properties
ylabel('Transmittance','FontSize',14)
xlabel('Phase difference (rad)','FontSize',14)
set(gca,'FontSize',14);  % size of tick marks on both axes
text(6.1, 0.05, '2 \pi','Fontsize',14)
text(12.2, 0.05, '4 \pi','Fontsize',14)
text(8.5, 0.1, 'r = 0.8','Fontsize',14)
text(8.5, 0.5, 'r = 0.4','Fontsize',14)
text(8.5, 0.8, 'r = 0.2','Fontsize',14)
%
pause
close all
```

## 电磁学基本知识

### 麦克斯韦方程组

#### 微分形式麦克斯韦方程组

$$
\nabla\times \bold{E}=-\frac{\part \bold{B}}{\part t}\\
\nabla\times\bold{H}=\bold{J}+\frac{\part \bold{D}}{\part t}\\
\nabla\cdot\bold{D}=\rho_v\\
\nabla\cdot\bold{B}=0
$$

其中
$$
\bold{E}:电场强度[V/m]\\
\bold{B}:磁通密度[T]\\
\bold{H}:磁场强度[A/m]\\
\bold{D}:电通密度[C/m^2]\\
\bold{J}:电流密度[A/m^2]\\
\rho_v:体积电荷密度[C/m^3]\\
笛卡尔坐标系下的算子\nabla:\nabla=[\frac{\part}{\part x},\frac{\part}{\part y},\frac{\part}{\part z}]
$$
且有
$$
\bold{D}=\varepsilon\bold{E}\\
\bold{B}=\mu\bold{H}\\
\bold{J}=\sigma\bold{E}\\
$$
其中
$$
\varepsilon:介电常数[F/m]\\
\mu:渗透率[H/m]\\
\sigma:电导率
$$

#### 高斯定理

$$
\oint\bold{F}\cdot ds=\int_V\nabla\cdot\bold{F}dv
$$

#### 斯托克斯定理

$$
\oint\bold{F}\cdot dl=\int_A\nabla\cdot\bold{F}d\bold{s}
$$

#### 积分形式麦克斯韦方程组

> 由上述两定理可将微分形式转为积分形式

$$
\oint_S\bold{D}d\bold{s}=\int_V\rho_vdv\\
\oint\bold{B}\cdot\bold{s}=0\\
\oint_L\bold{E}\cdot d\bold{l}=-\int\frac{\part\bold{B}}{\part t}\\
\oint_L\bold{H}\cdot d\bold{l}=\int_A\frac{\part\bold{D}}{\part t}+I
$$

- 介质性质主要由$~\varepsilon,\mu,\sigma~$决定
  - 对于介电介质，$~\varepsilon~$起主要作用
- $~\varepsilon~$与$~E~$无关时称为线性介质，否则非线性
- 不依赖空间上位置时称为均匀介质，否则非均匀
- 性质与方向无关，则介质为各向同性，否则为各向异性

### 边界条件

> 由麦克斯韦方程组的积分形式导出

![用于推导两种不同介质间场边界条件的轮廓和圆柱形状](../fig/PY00/PY00_chapter03_fig02.jpg)

- 将所有向量分为两个分量，一个平行于界面，一个垂直于界面
- 所示的轮廓和圆柱形状简化了边界条件的推导
  - 对于电场和磁场是独立的

#### 电场边界条件

$$
\frac{D_{1t}}{\varepsilon_{r1}}=\frac{D_{2t}}{\varepsilon_{r2}}
$$

#### 磁场边界条件

$$
\mu_{r1}H_{1n}=\mu_{r2}H_{2n}
$$

### 波动方程

> 无源介质的波动方程

![场的边界条件](../fig/PY00/PY00_chapter03_fig03.jpg)
$$
\nabla^2\bold{E}-\mu\varepsilon\frac{\part^2}{\part t^2}\bold{E}
$$

### 时谐场

$$
\bold{E}(\bold{r},t)=Re\{\bold{E}(\bold{r})e^{j\omega t}\}
$$

- $~\bold E(\bold{r})~$是$~\bold{E}(\bold{r},t)~$的相量形式，是一般复数

### 极化波

- 极化的特征：$\bold{E}$矢量在空间中某一点 (与传播方向正交的平面上)所作的曲线作为时间的函数
- 在一般情况下，产生的曲线是一个椭圆，因此波称为椭圆极化
- 在一定条件下，椭圆可以化为一个圆或一段直线 (波的偏振分别是圆偏振和线偏振)

#### 线性极化波

> 平面极化波

$$
\bold{E}=\bold{\hat{e}}E_0e^{i(\omega t-\bold{k\cdot r}+\phi)}
$$

#### 圆极化波和椭圆极化波

> 考虑沿正交方向振荡的两个平面波，叠加就可以形成复杂波、

$$
(\frac{E_y}{E_{0y}})^2+(\frac{E_x}{E_{0x}})^2=1
$$

- $~E(z,t)~$的端点将在空间的给定点上追踪一个椭圆 (右椭圆极化波)

![典型偏振态:(a)椭圆态，(b)圆态，(c)线性态](../fig/PY00/PY00_chapter03_fig04.jpg)

### 菲涅尔系数和相位

- 入射平面：入射波和反射波的传播方向与两种介质间的界面垂直的单位向量所形成的平面
- 菲涅耳系数：根据两种介质的入射角度和材料性质 (ε介电常数)推导出的反射系数和透射系数
- 菲涅尔相

$$
r=e^{-2/\phi}
$$

#### TE极化

![TE偏振的菲涅耳反射](../fig/PY00/PY00_chapter03_fig05.jpg)

边界条件要求总场$~\bold{E}~$和总场$~\bold{H}~$在界面两侧的切向分量相等
$$
E_{1i}+E_{1r}=E_{2t}\\
-H_{1i}\cos\theta_1+H_{1r}\cos\theta_1=-H_{2t}\cos\theta_2
$$


### 介质表面反射的极化

### 增反射涂层

### 布拉格透镜

### 坡印廷定理

## 平板波导

- 射线光学平板波导

- EM介质波导理论基础

- 波动方程平面波导宽

- 三层对称指导结构(TE模式)

- 任意三层非对称平面波导的一维模式

- 多层平板波导：一维方法

## 线性光纤和信号退化

- 几何光学描述

- 柱坐标下的光纤模

- 色散

- 传播过程中的脉冲色散

## 线性脉冲的传播

- 基本脉冲

- 半导体激光器的调制

- 有色散时脉冲传播方程的简单推导

- 线性脉冲的数学理论

- 脉冲的传播

## 光源

- 激光器概述

- 半导体激光器

- 速率方程

- 基于速率方程的分析

## 光放大器和掺铒光纤放大器 (EDFA)

- 一般特性

- 掺铒光纤放大器

- 掺铒光纤放大器的增益特性

## 半导体光放大器(SOA)

- 一般讨论

- 脉冲传播的SOA速率方程

- SOA的设计

- SOA的一些应用