---
title: CloudSim Example1
tags:
  - CloudSim
categories: 
  - 云计算
date: 2020-02-01
---

## 介绍

CloudSim是一个云计算基础架构和服务的建模和仿真框架，由Java语言编写，提供给研究人员做仿真实验。

## 主要特点

* 支持大型云计算数据中心的建模和仿真
* 支持对虚拟服务器主机进行建模和仿真，并具有可自定义的策略，用于向虚拟机提供主机资源
* 支持对应用程序容器进行建模和仿真
* 支持能源感知计算资源的建模和仿真
* 支持对数据中心网络拓扑和消息传递应用程序进行建模和仿真
* 支持动态插入模拟元素，停止和继续模拟
* 支持用于将主机分配给虚拟机的用户定义策略以及用于将主机资源分配给虚拟机的资源

<!-- more -->

## Example1

Inspect **ClouldSimExample1.java**. Study the code and try to get an overall feel for what it is doing (or supposed to do). You should focus on the following aspects: 

* Virtual Machine creation 
* Virtual Machine description
* Broker
* Cloudlet
* Data centre
* Simulation parameter setting
* Simulation output

`CloudSimExample1.java`主要创建了一个含有一个云主机的数据中心，并在其上运行一个云任务。以下是部分代码分析：

```java
public class CloudSimExample1 {
    public static void main(String[] args) {
        try {
            // 云用户数量
            int num_user = 1;
            // 用当前日期和时间初始化字段的日历
            Calendar calendar = Calendar.getInstance();
            // 事件追踪
            boolean trace_flag = false;
            
            // 初始化 CloudSim 工具包
            CloudSim.init(num_user, calendar, trace_flag);
            
            // 创建数据中心
            Datacenter datacenter0 = createDatacenter("Datacenter 0");
            
            // 创建 Broker 代理
            DatacenterBroker broker = createBroker();
            
            // 创建一个虚拟机列表
            vmlist = new ArrayList<Vm>();
            
            // 创建一个虚拟机
            Vm vm = new Vm(vmid, brokerId, mips, pesNumber, ram, bw, size, vmm, new CloudletSchedulerTimeShared());
            
            // 将虚拟机添加到虚拟机列表中
            vmlist.add(vm);
            
            // 将虚拟机列表提交到数据中心代理
            broker.submitVmList(vmlist);
            
            // 创建云任务列表
            cloudletList = new ArrayList<Cloudlet>();
            
            // 创建云任务
            Cloudlet cloudlet = new Cloudlet(id, length, pesNumber, fileSize, outputSize, utilizationModel, utilizationModel, utilizationModel);
			cloudlet.setUserId(brokerId);
			cloudlet.setVmId(vmid);
            
            // 将云任务添加到列表中
            cloudletList.add(cloudlet);
            
            // 将云任务列表提交到数据中心代理
            broker.submitCloudletList(cloudletList);
            
            // 开始模拟
            CloudSim.startSimulation();
            
            // 结束模拟
            CloudSim.stopSimulation();
            
            // 输出结果
            List<Cloudlet> newList = broker.getCloudletReceivedList();
            printCloudletList(newList);
        }
    }
    
    // 创建数据中心
    private static Datacenter createDatacenter(String name) {
        // 创建列表用于储存机器，简称主机列表
        List<Host> hostList = new ArrayList<Host>();
        
        // 创建处理器，并添加到Pe列表中
        peList.add(new Pe(0, new PeProvisionerSimple(mips)));
        
        // 创建处理器，并将其添加到主机列表中
        int hostId = 0;
        int ram = 2048;
        long storage = 1000000;
        int bw = 10000;
        
        hostList.add(new Host(hostId, new RamProvisionerSimple(ram), new BwProvisionerSimple(bw), storage, peList, new VmSchedulerTimeShared(peList)));
        
        // 创建数据中心特征，它表示了数据中心的静态属性：体系架构、操作系统、主机列表、分配策略、时间或空间共享、时区、价格
        
        // 创建Power数据中心
        Datacenter datacenter = null;
        try {
            datacenter = new Datacenter(name, characteristics, new VmAllocationPolicySimple(hostList), storageList, 0);
        } catch (Exception e) {
            e.printStackTrace();
        }
        return datacenter;
    }
    
    // 创建代理，可以根据特定需求发展自己的代理协议来提交虚拟机和云任务
    private static DatacenterBroker createBroker() {
        
    }
    
    // 打印
    private static void printCloudletList(List<Cloudlet> list) {
        
    }
}
```

