# 计算机网络-Ch2-物理层

####[全书笔记链接](https://www.zybuluo.com/omou/note/730705)
---
##目录
[TOC]

## 1 数据通信的理论基础
### 1.1 带宽
- （**模拟**）带宽：**Hz**
- （**数字**）带宽：**bps** - bits per seconds

### 1.2 奈奎斯特（Nyquist）采样定理*（理想信道）*：
- 最大数据速率 = **$2Blog_2V(bps)$** *（B为低通滤波器带宽，V为离散等级）*
### 1.3 香农（Shannon）定理*（有噪声信道）*：
- 最大数据速率 = **$Blog_2(1+\frac{S}{N})$** *（$\frac{S}{N}$为信噪比）*

## 2 数字调制与多路复用 - Multiplexing Digital Modulation
### 2.1 **基带传输** baseband transmission （电缆信道）

#### 2.1.1 **带宽效率**：
提高离散等级能提高贷款效率；带宽是有限资源；信号频率越高，衰减越大。

 - 符号率 = 比特率/每个符号的比特数 = 波特率
 - **NRZ** - Non-Return-to-Zero - 不归零编码：最简单
 
---
#### 2.1.2 **时钟回复**：
将数据信号与时钟信号结合增加信道利用率。

 - **曼彻斯特编码**：NRZ与始终信号异或，‘0’为上升沿，‘1’为下降沿。
 - **NRZI** - Non-Return-to-Zero-Inverted - 不归零逆转：‘0’为信号不变，‘1’为信号跳变（USB Universal Serial Bus）。
 
一长串1的检测问题可用NRZI解决，一长串0可用**4B/5B**编码和**扰频/倒频**编码解决。

- **4B/5B**：每4个bits映射为5个bits，拆分成串的0为更多的1
- **扰频器**（scrambler）：发送前用一个伪随机序列来异或信号
- **倒频器**：以同样的序列解释信号

---
#### 2.1.3 **平衡信号** ：
在很短的时间内正电压与负电压一样多的信号。

- **双极编码**：±1V表示‘1’，0V表示‘0’（**AMI** - Alternate Mark Inversion - 交替标记逆转，电话网络中的编码方法）

---
### 2.2 **通带传输** passband transmission （无线和光纤信道）
- **ASK** - Amplitude Shift Keying - 幅移键控
- **FSK** - Frequency Shift Keying - 频移键控
- **PSK** - Phase Shift Keying - 相移键控
  - **BPSK** - Binary ... - 二进制（两个符号，不是两个比特）...
  - **QPSK** - Quadrature ... - 正交（四个符号，两个比特）...
- **星座图** - constellation diagram：融合了调幅和调相。
  - **QAM-16** - Quadrature Amplitude Modulation - 正交调幅
  - **QAM-64** - $2^4$
  - **格雷码** - Gray code - 相邻符号只有一个bit的位置不同

### 2.3 **频分复用** - FDM - Frequency Division Multiplexing
每个用户独享一个频段（**OFDM** - Orthogonal Frequency Division Multiplexing - 正交频分复用）。

### 2.4 **时分复用** - TDM - Time Division Multiplexing
每个用户周期性地获得整个带宽非常短的一段时间。每个输入流的比特流从一个固定的**时间槽**（time slot）取出并输出到混合流。

### 2.5 **码分复用** - CDM - Code Division Multiplexing
将窄带信号扩展到很宽的频带上。更能容忍干扰，而且允许来自不同用户的多个信号共享相同的频带。由于码分复用技术最常用于第二个目的，因此它被称为**码分多址** - CDMA - Code Division Multiple Access。

这里是一个同步CDMA的例子。
设有四个码片序列（chip sequence)A,B,C,D供四个接收站使用：
$A = (-1-1-1+1+1-1+1+1)$
$B = (-1-1+1-1+1+1+1-1)$
$C = (-1+1-1+1+1+1-1-1)$
$D = (-1+1-1-1-1-1+1-1)$

$$S·T=\frac{1}{m}\sum^{m}_{i=1}S_iT_i=0 (S,T为码片序列）$$
$$S·S=\frac{1}{m}\sum^{m}_{i=1}S_i^2=1$$
则A发送‘1’，B发送‘1’，C发送‘0’，D发送‘1’：

$S=A+B+\bar C+D=(-2-2+0-2+0-2+4+0)$

接收方：
$a = S·A = A·A + B·A + \bar C·A + D·A = 1$
$b = ... = 1$
$c = ... = 0$
$d = ... = 1$

## 3 **PSTN** - Public Switched Telephone Network - 公共交换电话网络

长途呼叫的典型电路路由：
```graphTB
    a(电话) -->|本地回路| b(端局)
    b -->|长途连接中继线| c(长途局)
    c -->|超高带宽局间中继线| d(中间交换局)
    d --> e(...)
```
电话系统由以下三个主要部分构成：
1. 本地回路（进入家庭和公司的模拟双绞线）
2. 中继线（连接交换局的数字光纤）
3. 交换局（电话呼叫在这里从一条中继线被接入到另一条中继线）
### 3.1 本地回路：“最后一英里”
- 调制解调器：执行数字比特流和模拟信号流之间转换的设备
- 数字用户线 - ADSL
- 光纤到户

### 3.2 中继线和多路复用
#### 3.2.1 时分多路复用
PCM采样率为8000/s，125微秒/样值。北美和日本使用T1载波，基于PCM和TDM。每帧24*8+1个比特，24和信道。每125微秒一帧。
#### 3.2.2 **SONET/SDH**
**SONET** - Synchronous Optical NETwork - 同步光网络
**SDM** - Synchronous Digital Hierarchy - 同步数字系列
810 Bytes的SONET帧最好描述为90列宽、9行高的矩形，每秒8000帧，共51.84 Mbps。这是基本的SONET信道，成为**同步传输信号-1**（STS-1，Synchronous Transport Signal-1）。所有的SONET中继线都是STS-1的倍数。
#### 3.2.3 波分多路复用 - WDM - Wavelength Division Multiplexing
利用光纤的巨大带宽，将不同信道信号能量置于不同波长处，之后汇集到一条光纤传输。光纤带宽大约为25000GHz。

### 3.3 交换
#### 3.3.1 电路交换 - circuit switching
![电路交换](https://thumbnail0.baidupcs.com/thumbnail/c6085b947e6d95c74900ba899dbc9427?fid=521343134-250528-290910480926920&time=1492873200&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-HQc2vNRN%2BDblP%2FkEjma2PrnBBuY%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=2597154165505207528&dp-callid=0&size=c710_u400&quality=100)
#### 3.3.2 包交换 - package switching
![包交换](https://thumbnail0.baidupcs.com/thumbnail/1c5e6fb64a270ba3467f72ee8edddd03?fid=521343134-250528-631170404917032&time=1492873200&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-kdnsb2hex8KI7Nn5WE4q59tXvGk%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=2597165583111950941&dp-callid=0&size=c710_u400&quality=100)

---

|项目|电路交换|包交换|
|:----|:---:|:---:|
|呼叫建立|需要|不需要|
|专用物理路径|是|不是|
|每个包遵循相同的路由|是|不是|
|包按顺序到达|是|不是|
|交换机崩溃是否致命|是|不是|
|可用带宽|固定|动态|
|可能拥塞时间|在建立时|在每个包|
|潜在浪费带宽|有|没有|
|存储-转发传输|不是|是|
|收费|按分钟|按包|

## 4 移动电话系统
### 4.1 第一代移动电话 - **1G** - 模拟语音

- **AMPS** - Advanced Mobile Phone System - 高级移动电话系统：已退休，但是是2G和3G的基础。
- **（频率重用）**：一个地理区域被分为许多个**蜂窝（cell）**，在AMPS中每个跨度10~20 km，数字系统中要小一点。相邻的蜂窝不会使用相同的频率组，相近但不相邻的可以。
- **基站**：每个蜂窝一个基站,在一个小规模的系统中所有基站连接到**移动电话交换局（MTSO - Mobile Telephone Switching Office)**,向上有耳机MTSO，以此类推。
- **切换（handofff）**：电话从一个蜂窝切换到另一个蜂窝时，原蜂窝基站能检测到信号越来越弱，而后询问周围基站检测到的该电话信号功率谁最大，完成切换，耗时约300ms。
- **信道**：AMPS使用**FDD** - Frequency Division Duplex - 频分双工划分了832个全双工信道。

### 4.2 第二代移动电话 - **2G** - 数字语音
![frequency_reusing](https://thumbnail0.baidupcs.com/thumbnail/076118a1e03f6038ca649a030a80418b?fid=521343134-250528-712621910815612&time=1492912800&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-28EU3%2BAfdUbQ0VcOXMCMPcvJaw4%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=2607782603466322750&dp-callid=0&size=c710_u400&quality=100)
- **D-AMPS** - Digital AMPS - 数字高级移动电话系统：与AMPS共存，使用TDM。
- **GSM** - Global System for Mobile Communications - 全球移动通信系统
 - **SIM卡** - Subscriber Identity Module - 用户识别模块：用户账户信息，加密。
 - **空中接口 - air interface**
 - **基站控制器** - BSC - Base Station Controller
 - **访问位置寄存器** - VLR - Visitor Location Register：包括所有附近移动电话的数据库。
 - **归属位置寄存器** - HLR - Home Location Register：用来把入境呼叫路由到正确位置的数据库。
 
```graphLR
    a(SIM卡&手机) -->|空中接口| c(BSC)
    b(SIM卡&手机) -->|空中接口| c(BSC)
    d(HLR) --> f
    c --> f(MSC)
    e(VLR) --> f
    f --> g(PSTN)
```
（省略了具体的包交换过程的笔记）

### 4.3 第三代移动电话 - **3G** - 数字语音和数据
CDMA，WCDMA


##ABBREVIATION
**ADSL** - Asymmetric Digital Subscriber Line - 非对称用户数字线
**LATA** - Local Access and Transport Areas - 本地接入和传输区域
**LEC** - Local Exchange Carrier - 本地交换运营商
**IXC** - IntereXchange Carrier - 跨区运营商
**POP** - Point of Presence - 存点（交换局）
**ISP** - Internet Service Provider - 互联网服务提供商
**TCM** - Trellis Coded Modulation - 网格编码调制
**DMT** - Discrete MultiTone - 离散多音
**POTS** - Plain Old Telephone Service - 简单老式电话服务
**NID** - Network Interface Device - 网络接口设备
**DSLAM** - Digital Subscriber Line Access Multiplexer - 数字用户线路接入复用器
**ISDN** - Integrated Services Digital Network - 综合业务数字网
**PON** - Passive Optical Network - 无源光网络
**PCM** - Pulse Code Modulation - 脉冲编码调制
**ITU** - International Telecommunication Union - 国际电信联盟
