# TIDB 性能测试



## 作业内容

![image-20200823122611438](./pic/image-20200823122611438.png)



## topu环境



![image-20200823124042527](./pic/image-20200823124042527.png)

## 机器配置

> 类型: 虚拟机实例 X 5台
>
> CPU: i5-10400 / 2C
>
> 内存: 4GB
>
> 磁盘: 型号:SN750 SSD 大小: 30GB



### 部署首次性能测试

![image-20200823124730828](./pic/image-20200823124730828.png)

## sysbench

#### 导入命令

> sysbench oltp_update_non_index --config-file=config --threads=32 --tables=32 --table_size=10000 prepare

#### 性能测试

##### oldp_point_select

![image-20200823130523436](./pic/image-20200823130523436.png)

##### oldp_update_index

<img src="./pic/image-20200823130630982.png" alt="image-20200823130630982" style="zoom:80%;" />

##### oldp_read_only

![image-20200825063630779](./pic/image-20200825063630779.png)

##### TIDB监控截图

![image-20200823131611288](./pic/image-20200823131611288.png)

##### TIKV监控截图

![image-20200823131733327](./pic/image-20200823131733327.png)

![image-20200823131811182](./pic/image-20200823131811182.png)

![image-20200823131913493](./pic/image-20200823131913493.png)

![image-20200823131926963](./pic/image-20200823131926963.png)



### GO-TPC

#### tpcc

> go-tpc tpcc -H192.168.50.234 -P4000 -D tpcc --warehouses 8 prepare -T 8
>
> go-tpc tpcc -H192.168.50.234 -P4000 -D tpcc --warehouses 8 run -T 8
>
> go-tpc tpcc -H192.168.50.234 -P4000 -D tpcc --warehouses 8 check -T 8
>
> go-tpc tpcc -H192.168.50.234 -P4000 -D tpcc --warehouses 8 cleanup -T 8

![image-20200825072221862](./pic/image-20200825072221862.png)

#### TIDB监控

![image-20200825072751429](./pic/image-20200825072751429.png)

#### TIKV监控

![image-20200825072533466](./pic/image-20200825072533466.png)

![image-20200825072549518](./pic/image-20200825072549518.png)

![image-20200825072622083](./pic/image-20200825072622083.png)

![image-20200825072640743](./pic/image-20200825072640743.png)

#### tpch

>  go-tpc tpch prepare -H 192.168.50.234 -P 4000 -D tpch --sf 4
>
>  go-tpc tpch run -H 192.168.50.234 -P 4000 -D tpch --sf 4





#### 性能分析

![image-20200825082136443](./pic/image-20200825082136443.png)



> 猜测， 当前性能瓶颈主要在sql解析模块
