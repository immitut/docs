# 如何安装 Magisk 到 Pixel 4XL

1. [下载**对应版本**官方镜像](https://developers.google.cn/android/images#coral) 并解压（两次）提取 **boot.img** 到移动设备

2. 通过 [**Magisk Manager**](https://github.com/topjohnwu/Magisk/releases) => 安装 => 选择并修补一个文件 选择对应的 boot.img 修补（过程建议全局科学上网）得到 **magisk_patched.img**

3. 将 magisk_patched.img 移动到 PC 端对应的 [**platform-tools**](https://developer.android.google.cn/studio/releases/platform-tools) 目录下,通过命令行工具刷入修补好的新镜像

   ```cmd
   cmd

   adb reboot-bootloader

   fastboot flash boot magisk_patched.img

   fastboot reboot
   ```

4. Done & enjoy.

5. PS: 无线调试

   ```cmd
   // adb tcpip <端口号> 本机电脑端口，未占用即可
   // adb connect <手机IP地址>:<端口号>
   adb tcpip 555
   adb connect 192.168.199.142:41181
   ```
