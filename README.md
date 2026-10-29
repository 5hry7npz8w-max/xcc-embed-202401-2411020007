# 嵌入式系统实验仓库

| 项目 | 内容 |
| --- | --- |
| 姓名 | 郭大江 |
| 班级 | 24 电信一班 |
| 学号 | 2411020007 |
| 课程 | 嵌入式系统 |
| 实验平台 | STM32F407ZETx |
| 开发工具 | STM32CubeMX + Keil MDK-ARM |

## 一、仓库说明

本仓库是「嵌入式系统」课程的实验代码仓库。按课程要求，**所有实验统一放在这一个仓库内**，每个实验一个子文件夹，后续实验依次增加，不再新建多个仓库。

各实验工程均由 STM32CubeMX 生成（`.ioc` 为工程配置文件），使用 Keil MDK-ARM 打开 `MDK-ARM/<工程名>.uvprojx` 编译、下载。

## 二、目录结构

```text
xcc-embed-202401-2411020007/
├── README.md          # 仓库说明：姓名、班级、学号、实验总说明
├── .gitignore         # 过滤 CubeMX 临时文件与 Keil 编译中间产物
├── 0501_LedWater/     # 实验一：LED 流水灯
└── 0602_MatrixKey/    # 实验二：矩阵按键扫描与键值显示
```

每个实验文件夹的内部结构一致：

```text
<实验文件夹>/
├── <工程名>.ioc        # STM32CubeMX 工程配置
├── Core/               # 用户代码：main.c、gpio.c 及启动文件
├── Drivers/            # HAL 库与 CMSIS
└── MDK-ARM/            # Keil 工程：.uvprojx / .uvoptx
```

## 三、实验列表

### 实验一：LED 流水灯（`0501_LedWater`）

- **功能**：8 个 LED 接在 PF0~PF7，程序每隔 200 ms 依次点亮其中一盏，形成流水灯效果，循环往复。
- **关键代码**：`Core/Src/main.c` 的 `while (1)` 循环中用 `HAL_GPIO_WritePin()` 移位点亮 `GPIO_PIN_0 << i`。
- **实验现象**：8 个 LED 依次点亮并熄灭，循环流动。

### 实验二：矩阵按键（`0602_MatrixKey`）

- **功能**：4×3 矩阵键盘，行线 PE0~PE3、列线 PE4~PE6，采用逐行扫描法并加 10 ms 软件消抖，识别键值 `0~9`、`*`、`#`。
- **关键代码**：`Core/Src/main.c` 中的 `MatrixKey_Scan()`（扫描与消抖）与 `LED_ShowValue()`（用 8 位 LED 以二进制显示键值）。
- **实验现象**：按下不同按键，LED 以二进制形式显示对应键值。

## 四、编译与烧录

1. （可选）用 STM32CubeMX 打开对应 `.ioc` 查看或修改外设配置。
2. 用 Keil MDK-ARM 打开 `MDK-ARM/<工程名>.uvprojx`。
3. `Build`（F7）编译工程，`Download`（F8）烧录到开发板。
4. 编译产物（`Objects/`、`Listings/`、`*.axf`、`*.hex`、`*.map` 等）已被 `.gitignore` 过滤，不会提交到仓库，克隆后需在本地重新编译。

## 五、备注

实验报告、现象截图后续补充到各实验文件夹中。
