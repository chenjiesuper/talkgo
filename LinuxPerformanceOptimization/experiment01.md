# 案例
## 02
### 场景一：CPU 密集型进程
stress --cpu 1 --timeout 600
### 场景二：I/O 密集型进程
stress -i 1 --timeout 600
### 场景三：大量进程的场景
stress -c 8 --timeout 600
## 03|04
### 以10个线程运行5分钟的基准测试，模拟多线程切换的问题
sysbench --threads=10 --max-time=300 threads run
## 05
docker run --name nginx -p 10000:80 -itd feisky/nginx
docker run --name phpfpm -itd --network container:nginx feisky/php-fpm
ab -c 10 -n 100 http://192.168.0.10:10000/
ab -c 10 -n 10000 http://10.240.0.5:10000/
## 06
docker run --name nginx -p 10000:80 -itd feisky/nginx:sp
docker run --name phpfpm -itd --network container:nginx feisky/php-fpm:sp
ab -c 100 -n 1000 http://192.168.0.10:10000/
ab -c 5 -t 600 http://192.168.0.10:10000/
## 07|08
docker run --privileged --name=app -itd feisky/app:iowait
## 09|10
docker run -itd --name=nginx -p 80:80 nginx
hping3 -S -p 80 -i u100 192.168.0.30

---
# 工具
## 02
uptime mpstat、pidstat
## 03|04
vmstat 、 pidstat 和 /proc/interrupts
## 05
top pidstat perf
## 06
top、pidstat、pstree perf|execsnoop
## 07|08
dstat、pidstat ps strace perf pstree
## 09|10
[sar](https://blog.csdn.net/volitationlong/article/details/81741754)、tcpdump
