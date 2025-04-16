# Storage
> Last Updated: Apr 16, 2025

## 磁盘/硬盘(考)
Magnetic disk (Hard disk)
- 速度取决于那个盘(drive)能转多块 60 ~ 200 r/s
- Transfer rate: rate of data flow between drive and computer
- Positioning time: time to move disk arm to desired cylinder (seek time) and time for desired sector to rotate under the disk head (rotational latency)
Typically several ms
- Head crash: a failure that occurs when a head makes contact with its rotating platter, slashing its surface and cause permanent damage
### Disk Attachment
- Storage accessed through I/O ports talking to I/O busses
- SCSI
- SAS
- SATA
### Disk Scheduling
- 操作系统负责高效利用硬件——对于磁盘驱动器而言，这意味着拥有快速的访问时间和磁盘带宽。
  - 磁盘带宽(Disk bandwidth)：传输的**总字节数**除以首次服务请求和最后一次传输完成之间的**总时间**
- 访问时间包含两个部分：寻道时间 + 旋转延迟(Access time has two components: Seek time + Rotational latency )
- 目的: 最小化寻道时间(Seek time)
- 寻道时间 取决于 寻道距离
- Different algorithms to schedule the service of disk I/O requests
张三要去一条街上不同的房屋送牛奶, 它要怎么安排自己的送奶顺序?(通常张三不在路的两端, 且张三无法预知所有的需要送奶的门牌号)
- FCFS
- SSTF (最短seek时间优先)
  - May cause starvation of some requests, 比如一个请求特别远, 它就得一直等
- SCAN(又叫电梯算法)
  - 上楼的时候就一直上, 上到顶楼才下, 然后一直下, 之后又上...
- C-SCAN
  - 上到顶楼后瞬移到G楼
- C-LOOK
  - 不会每次都上到顶楼, 每次瞬移回的时候也不一定会到G楼

### Disk Formatting
- Low-level formatting (physical formatting):低级格式化（物理格式化）：
  - Dividing a disk into sectors that the disk controller can read and write 将磁盘划分为磁盘控制器可以读写的扇区
  - 为什么要低格?物理扇区可能损坏, 所有OS仍然需要了解哪些是能用的block
  - Logical formatting: “making a file system”
- 用于处理坏块的方法（例如使用扇区备用）
  - 每个磁道(track)保留一个备用扇区
  - 检测到错误写入后，数据将写入备用扇区，并将坏扇区标记为不可用

## Final Exam
- 2025 May 2, 14:00-16:00
- Similar to midterm
- Closed-book, paper-based
- Calculator allowed (on approval list)
- No computer/software
- Scope: all lectures and tutorials (Except SSD)

## SSD(optional, 不考)
