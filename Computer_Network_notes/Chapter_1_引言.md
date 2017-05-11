# 计算机网络-Ch1-引言

---

## 1.网络硬件

- **点到点链路** - Point to Point
- **广播式链路** - Boradcasting

1. **PAN** - Personal Area Network - 个域网：多个设备围绕一个人进行通信
2. **LAN** - Local Area Network - 局域网：私有网络，一般在一栋建筑内
   - **AP** - Access Point - 接入点：**无线路由器**（wireless router）；**基站**（base station）
   - **WiFi**：无线局域网的 IEEE 802.11标准
   - 点到点的无线拓扑结构
   - **以太网** - Ethernet：IEEE 802.3 有线局域网
3. **MAN** - Metropolitan Area Network - 城域网
4. **WAN** - Wide Area Network - 广域网
   - **主机，通信子网，交换机** - host，communication subnet，switch：路由器（router）
   - **NSP，ISP** - Network/Internet Service Provider - 网络/因特网服务提供商：子网经营者
 
## 2.网络软件
- **面向连接的服务** - connection-oriented service：通信前先建立连接
- **无连接的服务** - connectionless sevice：报文，数据包
- **存储-转发交换** - store-and-forward switching：一个包全部接受到才能向下一个节点转发
- **直通式交换** - cut-through switching：相反

## 3.参考模型
### **OSI** - Open Systems Interconnection - 开放系统互联
  1. **物理层** - physical layer
  2. **数据链路层** - data link layer
  3. **网络层** - network layer
  4. **传输层** - transport layer
  5. **会话层** - session layer
  6. **表示层** - persentation layer
  7. **应用层** - application layer ：HTTP（HyperText Transfer Protocol）
  
### OSI模型的核心：
**_服务_**：该层做什么，定义了该层的语义.
**_接口_**：告诉上一层的进程如何访问本层，规定了参数和结果.
**_协议_**：本内内部的事情，规定了如何工作，可随意更换不影响其他层.
  
### **TCP/IP** - TCP/IP Reference Model
  1. **链路层** - link layer：不是真正意义上的层，是主机与传输线路之间的一个接口。DSL，SONET，802.11，Ethernet
  2. **互联网层** - internet layer：IP，ICMP
  3. **传输层** - transport layer：主机间的对话，TCP，UDP
  4. **应用层** - application layer：HTTP，SMTP，RTP，DNS
  
### **本书使用的模型**

|层级   | 层名  |
| :-----: | :---------: |
| 5     |     应用层     |
| 4     |     传输层     |
| 3     |     网络层     |
| 2     |   数据链路层   |
| 1     |     物理层     |

## ABBREVIATION
- **VPN** - Virtual Private Networks - 虚拟专用网络
- **RFID** - Radio Frequency IDentification - 射频识别
- **GPS** - Global Positioning System - 全球定位系统
- **NFC** - Near Field Communication - 进场通信
- **DMCA** - Digital Millennium Copyright Act - 数字千年版权法案
- **CAPTCHA** - Compelety Auto Public Turing test to tell Computers and Humans Apart - 完全自动图灵测试
- **IP** - Internet Protocal - 因特网协议
- **ICMP** - Internet Control Message Protocal - 因特网控制报文协议
- **TCP** - Transport Control Protocol - 传输控制协议
- **UDP** - User Datagram Protocol - 用户数据报协议
