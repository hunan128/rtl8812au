# rtl8812au-ac openwrt 5.4.188内核的驱动
使用方法：
  删除rtl8812aau-at,安装此ipk
  存在的bug,安装后可以正常发射wifi,但是无法修改wifi参数（表现为修改保存应用设备就重启）
  只能通过scp的方式修改/etc/config/wireless然后保存重启生效。
  
 如果你们会编译openwrt也可以按照如下执行，则不会存在上面描述的bug。
 
 问题：设备插入如华硕AC56、三星W01等RTL8812AU芯片的扩展USB网卡，无法使能AP模式，具体表现为配置AP模式后，ifconfig wlan0无法查找到，重新扫描WiFi无法正常启动。但lsusb查看设备还存在。
解决：本地编译补丁文件
wget https://github.com/1Jeff1/openwrt/commit/af426db0e78c3880a6bfe26fa97ae03caccce783.patch
patch -p1 -i af426db0e78c3880a6bfe26fa97ae03caccce783.patch
make menuconfig
firmware-wireless-中取消选择8812au-ct,安住y选择8812au-ac 后保存
make 编译
测试正常开启AP模块。
只经过X86测试
