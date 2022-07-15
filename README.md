操作系统的实现

## 目标

1. 系统引导
2. 硬件及驱动
   - CPU
   - 显示器
   - 键盘
   - 时钟

3. 任务调度：进程，线程

4. 内存管理

5. 文件系统

6. 系统调用

7. shell

### 编译
      nasm -f bin boot.asm -o boot.bin
      

### 创建硬盘镜像
   创建硬盘镜像,16M的硬盘，512字节的扇区大小
      bximage -q -hd=16 -func=create -sectsize=512 -imgmode=flat master.img
   将 boot.bin 写入主引导扇区
      dd if=boot.bin of=master.img bs=512 count=1 conv=notrunc

### 配置bochs
   ata0-master: type=disk, path="master.img", mode=flat