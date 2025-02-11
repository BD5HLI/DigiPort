# 简介

面向八重洲FT-891的FT8模式集成接口，内置一个2口的USB2.0 HUB和一个USB声卡，通过一个Type-C接口连接电脑或者手机，解决FT-891没有内置声卡的问题。

本项目采用了Digirig-Mobile项目（https://github.com/softcomplex/Digirig-Mobile ）的符号库、封装库和3D器件模型，参考了Digirig DR-891的原理图（https://digirig.net/digirig-dr-891-setup-manual/ ）设计，精简了几乎用不到的CM108B GPIO脚的PTT功能，保留了VOX-PTT功能。此外，本项目的被动器件（电阻、电容）均采用0402手焊封装，便于手工焊接。

本项目虽然面向FT-891设计，实际上可以仅使用USB声卡的功能，从而适用于绝大多数带有音频输入输出接口的电台，比如K5、K6手台，配合相应的软件可以实现SSTV、APRS等玩法。

# 电路板渲染图

电路板正面：

![电路板正面](https://raw.githubusercontent.com/BD5HLI/DigiPort-891/refs/heads/main/resources/digiport-891-top.png "电路板正面")

电路板反面：

![电路板反面](https://raw.githubusercontent.com/BD5HLI/DigiPort-891/refs/heads/main/resources/digiport-891-bottom.png "电路板反面")

# 接口

DigiPort在电脑侧的接口为type c接口，可使用c to a或c to c数据线连接电脑或者手机；在电台侧的接口包括两个3.5mm的4芯TRRS接口，面向电路板器件面、type c接口在右侧时，左上的TRRS接口为音频/PTT接口，左下的TRRS接口为USB接口。

DigiPort的音频/PTT接口定义如下：  

```
   /\  
  |  |---------> 尖端   RIG_AFOUT 电台音频输出，接FT-891 DATA口的DATA OUT脚  
  |--|  
  |  |---------> 第一环 RIG_AFIN  电台音频输入，接FT-891 DATA口的DATA IN脚  
  |--|  
  |  |---------> 第二环 VOX_PTT   声控PTT，接FT-891 DATA口的PTT脚  
  |--|  
  |  |---------> 底部   GND       信号地，接FT-891 DATA口的GND脚  
__|  |__
|      |  
```

VOX_PTT信号用于没有USB串口的设备控制收发转换，控制源来自CM108B声卡的右声道，推荐采用1kHz或2kHz的单音作为VOX触发信号。

FT-891的DATA**插座**定义如下：

```
    /-----\      1脚：DATA OUT  
   / 6 _ 1 \     2脚：PTT  
  |5  |_|  2|    3脚：DATA IN  
   \ 4   3 /     4脚：GND  
    \-----/      5脚：SHIFT   
                 6脚：SQL   
```

DigiPort的电台侧USB接口定义如下：  

```
   /\  
  |  |---------> 尖端   +5V 电台USB口的+5V电源脚  
  |--|  
  |  |---------> 第一环 D-  电台USB口的D-脚  
  |--|  
  |  |---------> 第二环 D+  电台USB口的D+脚  
  |--|  
  |  |---------> 底部   GND 电台USB口的GND脚  
__|  |__  
|      |  
```

USB Type-B**插头**定义如下：

```
   /---------\       
  /           \     1脚：+5V    
  |   2    1   |   
  | |--------| |    2脚：D-  
  | |        | |   
  | |--------| |    3脚：D+  
  |   3    4   |   
  |------------|    4脚：GND  
```

# 各目录内容说明

- digiport-891目录下是kicad格式的原理图和PCB图。  
- endboard目录下是采用25mm * 25mm * 40mm对扣小铝壳的端板3D图纸。  
- 3D-models目录下是部分器件的3D模型，来自Digirig-Mobile项目。  
- footprints.pretty目录下是部分器件的封装库，来自Digirig-Mobile项目。  
- symbols目录下是部分器件的符号库，来自Digirig-Mobile项目。  

# 致谢

- 感谢LX6FB提供原版DR-891的照片。

- 感谢BG5ARO对端板设计提出了宝贵建议，并提供了CNC加工。

- 感谢BG5BQB提供了3D打印工艺的端板原型样件。
