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

### MATLAB代码

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

### MATLAB代码

|       函数名        |                   描述                   |
| :-----------------: | :--------------------------------------: |
| reflections_TE_TM.m |     基于菲涅耳方程绘制TE和TM模的反射     |
|     bragg_an.m      | 用解析方法绘制TE模布拉格反射镜的反射率谱 |

#### 基于菲涅耳方程的反射图

```matlab
% reflections_TE_TM.m
% Plot of reflections based on Fresnel equations
% TE and TM reflections
% cases of external reflection
clear all
n = 1.50;  % relative refractive index
N_max = 11;  % number of points for plot
t = linspace(0,1,N_max);  % creation of theta arguments
theta = (pi/2)*t;  % angles in radians
% Plot reflection coefficients
num_TE = cos(theta) - sqrt(n^2-(sin(theta)).^2 );
den_TE = cos(theta) + sqrt(n^2-(sin(theta)).^2 );
r_TE = num_TE./den_TE;  % Plot for TE mode
num_TM = n^2*cos(theta) - sqrt(n^2-(sin(theta)).^2 );
den_TM = n^2*cos(theta) + sqrt(n^2-(sin(theta)).^2 );
r_TM = num_TM./den_TM;  % Plot for TM mode
%
angle_degrees = (theta./pi)*180;
x_line = [0 max(angle_degrees)];  % needed to draw horizontal line
y_line = [0 0];  % passing through zero
plot(angle_degrees,r_TE,angle_degrees,r_TM, x_line, y_line, '-',...
'LineWidth',1.5)
xlabel('Angle of incidence','FontSize',14)
set(gca,'FontSize',14);  % size of tick marks on both axes
text(60, -0.6, 'r_{TE}','Fontsize',14)
text(60, -0.2, 'r_{TM}','Fontsize',14)
text(55, 0.1, '\theta_{Brewster}','Fontsize',14)
pause
close all
```

#### 确定TE模式下布拉格反射镜的反射率谱

```matlab
% File name: bragg_an.m
% Determines reflectivity spectrum of Bragg mirror for TE mode
% using analytical method
clear all
N = 10;  % number of periods
n_L = 1.45;  % refractive index
n_H = 2.25;  % refractive index
a_L = 259;  % thickness (nm)
a_H = 167;  % thickness (nm)
Lambda = a_L + a_H;  % period of the structure
lambda = 1000:10:2200;
k_L = 2*pi*n_L./lambda;
k_H = 2*pi*n_H./lambda;
%
a=exp(1i*a_H*k_H).*(cos(k_L*a_L)+(1i/2)*(k_H./k_L+k_L./k_H).*sin(k_L*a_L));
d=exp(-1i*a_H*k_H).*(cos(k_L*a_L)-(1i/2)*(k_H./k_L+k_L./k_H).*sin(k_L*a_L));
b = exp(-1i*a_H*k_H).*((1i/2)*(k_L./k_H - k_H./k_L).*sin(k_L*a_L));
c = exp(1i*a_H*k_H).*((1i/2)*(k_H./k_L - k_L./k_H).*sin(k_L*a_L));
%
K = (1/Lambda)*acos((a+d)/2);
tt = (sin(K*Lambda)./sin(N*K*Lambda)).^2;
denom = abs(c).^2 + tt;
R = abs(c).^2./denom;
plot(lambda,R,'LineWidth',1.5)
axis([1000 2200 0 1.2])
xlabel('Wavelenght (nm)','FontSize',14)
ylabel('Reflectivity','FontSize',14)
set(gca,'FontSize',14);  % size of tick marks on both axes
pause
close all
```

## 平板波导

### 射线光学平板波导

### EM介质波导理论基础

### 波动方程平面波导宽

### 三层对称指导结构(TE模式)

### 任意三层非对称平面波导的一维模式

### 多层平板波导：一维方法

### MATLAB代码

|    函数名     |        描述         |
| :-----------: | :-----------------: |
| b_V_diagram.m | 绘制平面波导的b-V图 |
|     a3L.m     | 三层平面波导的分析  |
|  func_asym.m  |   a3L.m使用的函数   |

|   函数名   |                  描述                  |
| :--------: | :------------------------------------: |
|   slab.m   | 驱动函数(决定道具。常量和字段配置文件) |
| lossless.m |          无损耗波导结构的数据          |
|  lossy.m   |          有损耗的波导结构数据          |
|  visser.m  |          Visser描述的结构数据          |
|  muller.m  |              实现穆勒方法              |
|   f_TE.m   |           建立TE场的超越方程           |
|  mesh_x.m  |               生成一维网               |
| refindex.m |      为每个网格点分配参考索引的值      |
| TE_field.m |          确定所有网格点的TE域          |

```matlab
% File name: b_V_diagram.m
% function which plots b-V diagram of a planar slab waveguide
clear all
N_max = 400;  % number of points for plot
b = linspace(0,1.0,N_max);
hold on
for nu = [0, 1, 2]
  for a = [0.0, 8.0,50.0];  % asymmetry coefficient
    % determine V
    V1 = atan(sqrt(b./(1-b)) );
    V2 = atan(sqrt((b+a)./(1.0-b)));
    V3 = 1./sqrt(1.0-b);
    V = (nu*pi + V1 + V2).*V3;
    %
    plot(V,b,'LineWidth',1.2)
    grid on
    axis([0.0 20.0 0.0 1.0])  % change axis limit
  end
end
box on  % makes frame around plot
xlabel ('V','FontSize',14);
ylabel('b','FontSize',14);
set(gca,'FontSize',14);  % size of tick marks on both axes
text(10, 0.96, '\nu=0','Fontsize',14)
text(10, 0.8, '\nu=1','Fontsize',14)
text(10, 0.55, '\nu=2','Fontsize',14)
%
text(0.1, 0.3, 'a=0','Fontsize',14)
text(2.5, 0.3, 'a=50','Fontsize',14)
%
text(3.3, 0.2, 'a=0','Fontsize',14)
text(5.8, 0.2, 'a=50','Fontsize',14)
%
text(6, 0.1, 'a=0','Fontsize',14)
text(8.8, 0.1, 'a=50','Fontsize',14)
pause
close all
```

```matlab
% File name: a3L.m
% Analysis for TE modes
% First, we conduct test plots to find ranges of beta where possible
% solutions exists. This is done in several steps:
% 1. Plots are done treating kappa_f as an independent variable
% 2. Ranges of kappa_f are determined where there are zeros of functions
% 3. Corresponding ranges of beta are determined
% 4. Searches are performed to find propagation constants
%
clear all
% Definition of structure
n_f  = 1.50;  % ref. index of film layer
n_s  = 1.45;  % ref. index of substrate
n_c  = 1.40;  % ref. index of cladding
lambda = 1.0;  % wavelength in microns
h  = 5.0;  % thickness of film layer in microns
a_c  = 2*h;  % thickness of cladding region
a_s  = 2*h;  % thickness of substrate region
%
k = 2*pi/lambda;  % wave number
kappa_f = 0:0.01:3.0;  % establish range of kappa_f
beta_temp = sqrt((n_f*k)^2 - kappa_f.^2);
beta_min = min(beta_temp);
beta_max = max(beta_temp);
% Before searches, we plot search function versus beta
beta = beta_min:0.001:beta_max; % establish range of beta
N = beta./k;
ff = func_asym(beta,n_c,n_s,n_f,k,h);
plot(beta,ff)
xlabel('\beta','FontSize',22);
ylabel('Search function','FontSize',22);
ylim([-10.0 10.0])
grid on
pause
close all
%
% From the above plot, one must choose proper search range for each mode.
% Search numbers provided below are only for the waveguide defined above.
% For different waveguide, one must choose different ranges
% for searches.
beta0 = fzero(@(beta) func_asym(beta,n_c,n_s,n_f,k,h),[9.40 9.41])
beta1 = fzero(@(beta) func_asym(beta,n_c,n_s,n_f,k,h),[9.35 9.37])
beta2 = fzero(@(beta) func_asym(beta,n_c,n_s,n_f,k,h),[9.27 9.29])
beta3 = fzero(@(beta) func_asym(beta,n_c,n_s,n_f,k,h),[9.17 9.18])
% Plot of field profiles
A_s = 1.0;
thickness = h + a_c + a_s;
beta_field = beta0; % Select appropriate propagation constant for plotting
gamma_s = sqrt(beta_field^2 - (n_s*k)^2);
gamma_c = sqrt(beta_field^2 - (n_c*k)^2);
kappa_f = sqrt((n_f*k)^2 - beta_field^2);
%
% In the formulas below for electric field E_y we have shifted
% x-coordinate by a_s
% We also 'reversed' direction of plot in the substrate region
NN = 100;
delta = thickness/NN;
x = 0.0:delta:thickness;  % coordinates of plot points
x_t = 0;
for i=1:NN+1
  x_t(i+1)= x_t(i) + delta;
  if (x_t(i)<=a_s);
  	E_y(i) = A_s*exp(gamma_s*(x_t(i)-a_s));
  elseif (a_s<=x_t(i)) && (x_t(i)<=a_s+h);
  	E_y(i) = A_s*(cos(kappa_f*(x_t(i)-a_s))+...
  	gamma_s*sin(kappa_f*(x_t(i)-a_s))/kappa_f);
  else (a_s+h<=x_t(i)) & (x_t(i)<=thickness);
  	E_y(i) = A_s*(cos(kappa_f*h)+gamma_s*sin(kappa_f*h)/kappa_f)...
  	*exp(-gamma_c*(x_t(i)-h-a_s));
  end
end
%
h=plot(x,E_y);
% add text on x-axix and y-axis and size of x and y labels
xlabel('x (microns)','FontSize',22);
ylabel('TE electric field','FontSize',22);
set(h,'LineWidth',1.5);  % new thickness of plotting lines
set(gca,'FontSize',22);  % new size of tick marks on both axes
grid on
pause
close all
```

```matlab
function f = func_asym(beta,n_c,n_s,n_f,k,h)
% Construction of search function for asymmetric 3-layers waveguide
%
gamma_c = sqrt(beta.^2 - (n_c*k)^2);
gamma_s = sqrt(beta.^2 - (n_s*k)^2);
kappa_f = sqrt((n_f*k)^2 - beta.^2);
%
denom = kappa_f - (gamma_c.*gamma_s)./kappa_f;
f = tan(kappa_f*h) - (gamma_s+gamma_c)./denom;
```

```matlab
% File name: slab.m
% Driver function which determines propagation constants and
% electric field profiles (TE mode) for multilayered slab structure
clear all;
format long
% Input structure for analysis (select appropriate input)
%lossless;
%lossy;
visser
%
epsilon = 1e-6;  % numerical parameter
TE_mode = [];
n_max = max(n_layer);
z1 = n_max;  % max value of refractive index
n_min = max(n_s,n_c) + 0.001;  % min value of refractive index
dz = 0.005;  % iteration step
mode_control = 0;
%
while(z1 > n_min)
      z0 = z1 - dz;  % starting point for Muller method
      z2 = 0.5*(z1 + z0);  % starting point for Muller method
      z_new = muller(@f_TE , z0, z1, z2);
    if (z_new ~= 0)
    % verifying for mode existence
    for u=1 : length(TE_mode)
      if(abs(TE_mode(u) - z_new) < epsilon)
        mode_control = 1; break; % mode found
      end
    end
    if (mode_control == 1)
      mode_control = 0;
    else
      TE_mode(length(TE_mode) + 1) = z_new;
    end
  end
z1 = z0;
end
%
TE_mode = sort(TE_mode, 'descend');
%TE_mode'  % outputs all calculated modes
beta = TE_mode(2);  % selects mode for plotting field profile
x = mesh_x(d_s,d_layer,d_c,NumberMesh);
n_total = [n_s,n_layer,n_c];  % ref index for all layers
n_mesh = refindex(x,NumberMesh,n_total);
TE_mode_field = TE_field(beta,n_mesh,x,k_0);
```

```matlab
% File name: lossless.m
% Contains data for lossless waveguide
% Reference:
% J. Chilwell and I. Hodgkinson,
% "Thin-films field-transfer matrix theory of planar multilayer
% waveguides and reflection from prism-loaded waveguide",
% J. Opt. Soc. Amer.A, vol.1, pp. 742-753 (1984).
% Fig.3
% Global variables to be transferred to function f_TE.m
%
global n_c  % ref. index cladding
global n_layer  % ref. index of internal layers
global n_s  % ref. index substrate
global d_c  % thickness of cladding (microns)
global d_layer  % thicknesses of internal layers (microns)
global d_s  % thickness of substrate (microns)
global k_0  % wavenumber
global NumberMesh  % number of mesh points in each layer
% (including substrate and cladding)
n_c  = 1.0;
n_layer  = [1.66 1.60 1.53 1.66];
n_s  = 1.5;
d_c  = 0.5;
d_layer  = [0.5 0.5 0.5 0.5];
d_s  = 1.0;
NumberMesh = [10 10 10 10 10 10];
lambda  = 0.6328; % wavelength in microns
k_0  = 2*pi/lambda;
```

```matlab
% File name: lossy.m
% Contains data for lossy waveguide.
% Reference:
% C. Chen et al, Proc. SPIE, v.3795 (1999)
% Global variables to be transferred to function f_TE.m
global n_c  % ref. index cladding
global n_layer  % ref. index of internal layers
global n_s  % ref. index substrate
global d_c  % thickness of cladding (microns)
global d_layer  % thicknesses of internal layers (microns)
global d_s  % thickness of substrate (microns)
global k_0  % wavenumber
global NumberMesh  % number of mesh points in each layer
% (including substrate and cladding)
n_c  = 1.0;
n_layer  = [3.16455 3.22534 3.39583 3.5321-1j*0.08817 3.39614 3.38327];
n_s  = 3.172951;
d_c  = 1.0;
d_layer  = [0.6 1.6 0.518 0.6 0.2 0.1];
d_s  = 1.0;
NumberMesh = [10 10 10 10 10 10 10 10];
lambda  = 1.523; % wavelength in microns
k_0  = 2*pi/lambda;
```

```matlab
% File name: visser.m
% Contains data for five-layer waveguide with gain and losses
% Reference:
% T.D. Visser et al, JQE v.31, p.1803 (1995)
% Fig.6
% Global variables to be transferred to function f_TE.m
%
global n_c  % ref. index cladding
global n_layer  % ref. index of internal layers
global n_s  % ref. index substrate
global d_c  % thickness of cladding (microns)
global d_layer  % thicknesses of internal layers (microns)
global d_s  % thickness of substrate (microns)
global k_0  % wavenumber
global NumberMesh % number of mesh points in each layer
% (including substrate and cladding)
n_c  = 1.0;
n_layer  = [3.40-1i*0.002 3.60+1i*0.010 3.40-1i*0.002];
n_s  = 1.0;
d_s  = 0.4;
d_layer  = [0.6 0.4 0.6];
d_c  = 0.5;
NumberMesh = [10 10 10 10 10];
lambda  = 1.3; % wavelength in microns
k_0  = 2*pi/lambda;
```

```matlab
function f_val = muller (f, x0, x1, x2)
% Function implements Muller's method
iter_max = 100;  % max number of steps in Muller method
f_tol  = 1e-6;  % numerical parameters
x_tol = 1e-6;
y0 = f(x0);
y1 = f(x1);
y2 = f(x2);
iter = 0;
while(iter <= iter_max)
  iter = iter + 1;
  a =( (x1 - x2)*(y0 - y2) - (x0 - x2)*(y1 - y2)) / ...
  ( (x0 - x2)*(x1 - x2)*(x0 - x1) );
  %
  b = ( ( x0 - x2 )^2 * ( y1 - y2 ) - ( x1 - x2 )^2 *  ( y0 - y2 ) ) / .  .  .
  ( (x0 - x2)*(x1 - x2)*(x0 - x1) );
  %
  c = y2;
  %
  if (a~=0)
    D = sqrt(b*b - 4*a*c);
    q1 = b + D  ;
    q2 = b - D  ;
    if (abs(q1) < abs(q2))
      dx = - 2*c/q2;
    else
      dx = - 2*c/q1;
    end
    elseif (b~=0)
      dx = -c/b;
  else
    warning('Muller method failed to find a root')
    break;
  end
  x3 = x2 + dx;
  x0 = x1;
  x1 = x2;
  x2 = x3;
  y0 = y1;
  y1 = y2;
  y2 = feval(f, x2);
  if (abs(dx) < x_tol && abs (y2) < f_tol)
    break;
  end
end
% Lines below ensure that only proper values are calculated
if (abs(y2) < f_tol)
	f_val = x2;
	return;
else
	f_val = 0;
end
```

```matlab
function result = f_TE(z)
% Creates function used to determine propagation constant
% Variable description:
% result - expression used in search for propagation constant
% z  - actual value of propagation constant
%
% Global variables:
% Global variables are used to transfer values from data functions
global n_s  % ref. index substrate
global n_c  % ref. index cladding
global n_layer  % ref. index of internal layers
global d_layer  % thicknesses of internal layers (microns)
global k_0  % wavenumber
%
zz=z*k_0;
NumLayers = length(d_layer);
%
% Creation for substrate and cladding
gamma_sub=sqrt(zz^2-(k_0*n_s)^2);
gamma_clad=sqrt(zz^2-(k_0*n_c)^2);
%
% Creation of kappa for internal layers
kappa=sqrt(k_0^2*n_layer.^2-zz.^2);
temp = kappa.*d_layer;
%
% Construction of transfer matrix for first layer
cc = cos(temp);
ss = sin(temp);
m(1,1) = cc(1);
m(1,2) = -1j*ss(1)/kappa(1);
m(2,1) = -1j*kappa(1)*ss(1);
m(2,2) = cc(1);
%
% Construction of transfer matrices for remaining layers
% and multiplication of matrices
for i=2:NumLayers
  mt(1,1) = cc(i);
  mt(1,2) = -1j*ss(i)/kappa(i);
  mt(2,1) = -1j*ss(i)*kappa(i);
  mt(2,2) = cc(i);
  m = mt*m;
end
%
result = 1j*(gamma_clad*m(1,1)+gamma_sub*m(2,2))...
		+ m(2,1) - gamma_sub*gamma_clad*m(1,2);
```

```matlab
function x = mesh_x(d_s,d_layer,d_c,NumberMesh)
% Generates one-dimensional mesh along x-axis
% Variable description:
% Input
% d_layer  - thicknesses of each layer
% NumberMesh - number of mesh points in each layer
% Output
% x  - mesh point coordinates
%
d_total = [d_s,d_layer,d_c];  % thicknesses of all layers
NumberOfLayers = length(d_total); % determine number of layers
delta = d_total./NumberMesh;  % separation of points for all layers
%
x(1) = 0.0;  % coordinate of first mesh point
i_mesh = 1;
for k = 1:NumberOfLayers  % loop over all layers
  for i = 1:NumberMesh(k)  % loop within layer
    x(i_mesh+1) = x(i_mesh) + delta(k);
    i_mesh = i_mesh + 1;
  end
end
```

```matlab
function n_mesh = refindex(x,interface,index_layer)
% Assigns the values of refractive indices to mesh points
% in all layers
% Input
% x()  -- mesh points coordinates
% interface(n) -- number of mesh points in layers
% index_layer() -- refrective index in layers
% Output
% index_mesh  -- refractive index for each mesh point
%
% Within a given layer, refractive index is assigned the same value.
% Loop scans over all mesh points.
% For all mesh points selected for a given layer, the same
% value of refractive index is assigned.
%
N_mesh = length(x);
NumberOfLayers = length(index_layer);
%
i_mesh = 1;
for k = 1:NumberOfLayers  % loop over all layers
  for i = 1:interface(k)  % loop within layer
    n_mesh(i_mesh+1) = index_layer(k);
    i_mesh = i_mesh + 1;
	end
end
```

```matlab
function TE_mode_field = TE_field(beta,index_mesh,x,k_zero)
% Determines TE optical field for all layers
%
% x - grid created in mesh_x.m
TotalMesh = length(x); % total number of mesh points
%
zz=beta*k_zero;
%
% Creation of constants at each mesh point
kappa = 0;
for n = 1:(TotalMesh)
  kappa(n)=sqrt((k_zero*index_mesh(n))^2-zz^2);
end
%
% Establish boundary conditions in first layer (substrate).
% Values of the fields U and V are numbered by index not by
% location along x-axis.
% For visualization purposes boundary conditions are set at first point.
U(1) = 1.0;
temp = imag(kappa(1));
if(temp<0), kappa(1) = - kappa(1);
end
% The above ensures that we get a field decaying in the substrate
V(1) = kappa(1);
%
for n=2:(TotalMesh)
  cc=cos( kappa(n)*(x(n)-x(n-1)) );
  ss=sin( kappa(n)*(x(n)-x(n-1)) );
  m(1,1)=cc;
  m(1,2)=-1i/kappa(n)*ss;
  m(2,1)=-1i*kappa(n)*ss;
  m(2,2)=cc;
  %
  U(n)=m(1,1)*U(n-1)+m(1,2)*V(n-1);
  V(n)=m(2,1)*U(n-1)+m(2,2)*V(n-1);
end
%
TE_mode_field = abs(U);  % Finds Abs(E)
max_value = max(TE_mode_field);
h = plot(x,TE_mode_field/max_value); % plot normalized value of TE field
% adds text on x-axix and size of x label
xlabel('x (microns)','FontSize',22);
% adds text on y-axix and size of y label
ylabel('TE electric field','FontSize',22);
set(h,'LineWidth',1.5);  % new thickness of plotting lines
set(gca,'FontSize',22);  % new size of tick marks on both axes
pause
close all
```

## 线性光纤和信号退化

### 几何光学描述

### 柱坐标下的光纤模

### 色散

### 传播过程中的脉冲色散

### MATLAB代码

#### 第一类贝塞尔函数作图

```matlab
% File name: bessel_J.m
% Plot of Bessel functions of the first kind J_m(z)
clear all
N_max = 101;  % number of points for plot
z = linspace(0,10,N_max);  % creation of z arguments
%
hold on
for m = [0 1 2]  % m - order of Bessel function
  J = BESSELJ(m,z);
  h = plot(z,J);
% Redefine figure properties
xlabel('z','FontSize',22);
ylabel('J_m(z)','FontSize',22);
text(1.1, 0.85, 'm = 0','Fontsize',18);
text(1.8, 0.65, 'm = 1','Fontsize',18);
text(3, 0.55,  'm = 2','Fontsize',18);
grid on
box on
%
set(h,'LineWidth',1.5);  % new thickness of plotting lines
set(gca,'FontSize',22);  % new size of tick marks on both axes
end
pause
close all
```

#### 第二类贝塞尔函数作图

```matlab
% File name: bessel_Y.m
% Plot of Bessel functions of the second kind Y_m(z)
clear all
N_max = 101;  % number of points for plot
z = linspace(0.01,10,N_max);  % creation of z arguments
%
hold on
for m = [0 1 2]  % m - order of Bessel function
Y = BESSELY(m,z);
h = plot(z,Y);
% Redefine figure properties
xlabel('z','FontSize',22);
ylabel('Y_m(z)','FontSize',22);
text(2.0, 0.7, 'm = 0','Fontsize',18);
text(3.5, 0.7, 'm = 1','Fontsize',18);
text(5.0, 0.7, 'm = 2','Fontsize',18);
axis([0 10 -5 1.5]);
grid on
box on
%
set(h,'LineWidth',1.5);  % new thickness of plotting lines
set(gca,'FontSize',22);  % new size of tick marks on both axes
end
pause
close all
```

#### 第二类修正贝塞尔函数作图

```matlab
% File name: bessel_K.m
% Plot of modified Bessel functions of the second kind K_m(z)
clear all
N_max = 101;  % number of points for plot
z = linspace(0.01,3,N_max);  % creation of z arguments
%
hold on
for m = [0 1 2]  % m - order of Bessel function
  K = BESSELK(m,z);
  h = plot(z,K);
% Redefine figure properties
xlabel('z','FontSize',22);
ylabel('K_m(z)','FontSize',22);
text(0.2, 0.8, 'm = 0','Fontsize',18);
text(1.0, 0.8, 'm = 1','Fontsize',18);
text(1.5, 0.8, 'm = 2','Fontsize',18);
axis([0 3 0 5]);
grid on
box on
%
set(h,'LineWidth',1.5);  % new thickness of plotting lines
set(gca,'FontSize',22);  % new size of tick marks on both axes
end
pause
close all
```

#### 第一类修正贝塞尔函数作图

```matlab
% File name: bessel_I.m
% Plot of modified Bessel functions of the first kind I_m(z)
clear all
N_max = 101;  % number of points for plot
z = linspace(0,3,N_max);  % creation of z arguments
%
hold on
for m = [0 1 2]  % m - order of Bessel function
  Y = BESSELI(m,z);
  h = plot(z,Y);
% Redefine figure properties
xlabel('z','FontSize',22);
ylabel('I_m(z)','FontSize',22);
text(1.1, 1.7, 'm = 0','Fontsize',18);
text(1.75, 1.7, 'm = 1','Fontsize',18);
text(2.4, 1.7, 'm = 2','Fontsize',18);
grid on
box on
%
set(h,'LineWidth',1.5);  % new thickness of plotting lines
set(gca,'FontSize',22);  % new size of tick marks on both axes
end
pause
close all
```

#### 确定函数并绘制模式HE_11的通用关系

```matlab
% File name: HE11.m
% Function determines and plots universal relation for mode HE_11
clear all
format long
% It works in the range of V = [0.50 2.4]
N_max = 190;
for n = 1:N_max
  VV(n) = 0.50 + n*0.01;
  V = VV(n);
  b_c(n) = fzero(@(b) func_HE11(b,V),[0.0000001 0.8]);
end
%
hold on
h1 = plot(VV,b_c);  % plots b =b(V)
%
temp1 = VV.*b_c;
dy1 = diff(temp1)./diff(VV);
Vnew1 = VV(1:length(VV)-1);
h2 = plot(Vnew1,dy1);  % plots first derivative
%
temp2 = dy1;
dy2 = diff(temp2)./diff(Vnew1);
Vnew2 = Vnew1(1:length(Vnew1)-1);
h3 = plot(Vnew2,Vnew2.*dy2);  % plots second derivative
%
text(2.3, 0.6, 'b','Fontsize',16);
text(1.8, 1.2, '{d(bV)}/{dV}','Fontsize',16);
text(0.25, 1.3, 'V{d^{2}(bV)}/{dV^{2}}','Fontsize',16);
axis([0 2.5 0 1.5]);
% Redefine figure properties
xlabel('V','FontSize',22);
grid on
box on
set(h1,'LineWidth',1.5);  % new thickness of plotting lines
set(h2,'LineWidth',1.5);
set(h3,'LineWidth',1.5);
set(gca,'FontSize',22);  % new size of tick marks on both axes
pause
close all
```

#### 定义基本关系的函数

```matlab
function result = func_HE11(b,V)
% Function name: func_HE11.m
% Function which defines basic relation
u= V*sqrt(1-b);
J1 = BESSELJ(1,u);
J0 = BESSELJ(0,u);
%
w = V*sqrt(b);
K1 = BESSELK(1,w);
K0 = BESSELK(0,w);
lhs = J1./J0;
rhs = (w./u).*(K1./K0);
result = lhs - rhs;
```



## 线性脉冲的传播

### 基本脉冲

### 半导体激光器的调制

### 有色散时脉冲传播方程的简单推导

### 线性脉冲的数学理论

### 脉冲的传播

### MATLAB代码

## 光源

### 激光器概述

### 半导体激光器

### 速率方程

### 基于速率方程的分析

### MATLAB代码

## 光放大器和掺铒光纤放大器 (EDFA)

### 一般特性

### 掺铒光纤放大器

### 掺铒光纤放大器的增益特性

### MATLAB代码

## 半导体光放大器(SOA)

### 一般讨论

### 脉冲传播的SOA速率方程

### SOA的设计

### SOA的一些应用

### MATLAB代码

## 光学接收器

### 主要特性

### 光电探测器

### 接收器分析

### 光电接收器建模

### MATLAB代码

## 有限差分时域 (FDTD)公式

### 一般公式

### 无离差的一维Yee实现

### 一维边界条件

### 无离差的二维Yee实现

### 二维吸收边界条件

### 离差

### MATLAB代码

## 光束传播法 (BPM)

### 近轴公式

### 一般理论

### 1+1维FD-BPM公式

### 结束语

### MATLAB代码

## 一些波分复用 (WDM)设备

### WDM系统基础

### WDM基础技术

### BPM在光子器件中的应用

### MATLAB代码

## 光链路

### 光通信系统

### 光链路

### 的设计

### 链路性能的测量

### 光纤作为线性系统

### 基于滤波功能的光链路模型

### MATLAB代码

## 光孤子

### 非线性光学极化率

### 主要非线性效应

### 非线性薛定谔方程的推导

### 分步傅里叶方法

### 数值结果

### 关于孤子通信的几点评论

### MATLAB代码

## 太阳能电池

### 简介

### 光伏发电原理

### 太阳能电池等效电路

### 多结结构

### MATLAB代码

## 超材料

### 简介

### Veselago方法

### 如何创造超材料

### 超材料的一些应用

### 具有活性元素的超材料

### MATLAB代码

# 附录

## MATLAB基础

### 基本规则

### MATLAB中良好编程的一些规则

### 基本图形

### 基本输入输出

### 数值微分

## 基本数值方法

### 一元牛顿法

### 穆勒方法

### 数值微分

### 龙格-库塔 (RK)方法

### 解微分方程

### 数值积分

### MATLAB中的符号集成

### 傅里叶级数

### 傅里叶变换

### FFT