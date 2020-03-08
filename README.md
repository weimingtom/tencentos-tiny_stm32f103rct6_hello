# tencentos-tiny_stm32f103rct6_hello
[WIP] The TencentOS Tiny hello MDK4 (Keil 4) project porting to zhongjingyuan stm32f103rct6 develop board

## Original From  
* https://github.com/Tencent/TencentOS-tiny/tree/a787b64f5144fcb05c14c4c1b057302d635c9857  
2019-09-20 a787b64 (commit 27)      
https://gitee.com/weimingtom/TencentOS-tiny  

## MDK4 (Keil4) Project  
* see projects/helloworld.uvproj  
* see readme.txt  

## Change debug serial from USART2 to USART1  
* search USART_DEBUG, if USART_DEBUG==1, use USART1 for debug serial     
* some LEDs and buttons define, see readme.txt  

## Step Debug  
* Please choose SW (SWD) instead of JTAG in J-Link setting dialog in MDK4    
