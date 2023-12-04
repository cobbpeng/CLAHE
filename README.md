# CLAHE
CLAHE in verilog


Open source 

CLAHE   on  FPGA  with  verilog HDL ,into blocks of size 8 * 8


1， Generally， input  data of video is Y(YUV) , so  you can give your image in gray for test  




1 , introduce
IP version   :  00 
IP function  ： implement the CLAHE algorithm with verilogHDL .  Divide images into blocks of size 8 * 8  
Latency    ： 26 clock 
Resolution  ：1920*1080 
Standards   ：VESA 
Hardware   ： xilinx all device
Software    ： vivado2022.1 
File type     ： DCP 
IP import    ： NO  (Except for DSP used by implementation instructions )
  Utilization    :    LUT       8.6k
                   LUTRAM   41  
                   FF        13K 
                   BRAM     64 
                   DSP       143 
                   (most of DSP used in module can be replaced with LUT )

2, Interface description 
//------------------------------------------------------------------------------------------------------------------------------------------------
//IO name        |    	Width    | 	Default value 	 |  Function 
//------------------------------------------------------------------------------------------------------------------------------------------------
//I_video_clk	   |        1		   |                   |  Input clock by video clock . such as 148.5M in 1080p 
//I_video_syn	   |        3	     |                   |  Input video synchronization signal follow VESA 
//I_video_dat	   |        8		   |                   |  Fix to 8bit because of DCP file generation limit 
//I_limit_dat	   |        32	   |     32’d4096	     |  Limit data for CLAHE , you can fix to 32’d633 and video will be more dark 
//I_hist_level	 |        4      |	    4’d2	       |  Ratio of CLAHE data in OUTPUT data 
                                                        0  :  Output data =    Original data  
                                                        1  :  Output data = 25% CLAHE data  +  75% Original data  
                                                        2  :  Output data = 50% CLAHE data  +  50% Original data 
                                                        3  :  Output data = 75% CLAHE data  +  25% Original data 
                                                        4  :  Output data =     CLAHE data 
//O_video_dat	  |      8	      |                    |  	Output data for video 
//O_video_syn   |     3		      |                    |    Output synchronization signal  for video 
// ---------------------------------------------------------------------------------------------------------------------------------------------



3, usage
3.1  Generate simulation file with DCP  
1)Open vivado and source into the directory , enter the command to tcl consoles as follows : 
    cd [get_property directory ]/clahe_dcp_top.dcp  
2)Open DCP file with vivado by open_checkpoint command :
open_checkpoint clahe_dcp_top.dcp
3)In the new window,  enter the following command
write_verilog -force -mode funcsim clahe_dcp_top_sim.v 
3.2  Import file to vivado 
Import DCP in design sources and simulation file to simulation sources 
   (more information about DCP and EDF , please contact www.xilinx.com )


4, supplement 
1, Setting to other resolution or data width , or any further questions, please feel free to contact me.
   Email : pengmoon19@gmail.com  

