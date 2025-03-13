# tmc2240-pcb
tmc2240-pcb, lceda, 3d printer driver.

![](https://github.com/wybliw/tmc2240-pcb/blob/main/tmc2240-pic.png)

LCEDA url: https://oshwhub.com/wybliw/tmc2240-qu-dong

在MKS怪兽8主板上使用最新klipper固件，驱动设置SPI和UART模式测试OK。

切换UART模式：焊接RUEN电阻，将RCS电阻换到电阻RUT上。

若出现欠压错误，添加 `driver_TPFD: 0` ，驱动采样电阻 `rref: 12000` ，不要设置错误。



**SPI配置：**

```
[tmc2240 stepper_x]
spi_software_mosi_pin: PE14
spi_software_miso_pin: PE13
spi_software_sclk_pin: PE12
cs_pin: PE6
run_current: 0.50
interpolate: False
stealthchop_threshold: 0
rref: 12000
diag0_pin: ^!PA14     # 无限位配置
driver_SGT: 3
driver_TPFD:0
```


**UART配置：**

```
[tmc2240 stepper_x]
uart_pin: PE6
uart_address: 7    # 默认地址要指定为 7 
run_current: 0.50
interpolate: False
stealthchop_threshold: 0
rref: 12000
diag0_pin: ^!PA14    # 无限位配置
driver_SGT: 3
driver_TPFD:0
```


**无限位配置：**

```
endstop_pin: tmc2240_stepper_x: virtual_endstop
```


注：驱动模块在UART下，由于AD0、AD1、AD2内部上拉，UART地址默认为7。一定要指定uart地址，

否则可能会出现通信错误：`Unable to read tmc uart 'stepper_x' register IFCNT` 。


