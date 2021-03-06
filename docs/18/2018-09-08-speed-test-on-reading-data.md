---
title: 两种数据处理方式时间对比
layout: post
date: 2018-09-17
---
近来工作中遇到了一个数据加载的问题，情况是百万级的数据存储在数据库中，多张表且表之间有关联。现需要使用Java读取表中数据并作关联后生成XML文件。有两种方案备选，一种是将多张表的数据分别读取到内存中，在内存中做关联，第二种是使用left join的方式在SQL层面就查询出数据，通过myBatis的ORM直接映射成Java对象。因为不确定哪一种方式读取的更快，做了如下实验：

1. 在数据库中创建两张大约10w数据的表。（通过存储过程插入数据，存储过程附在下面）
2. 分别使用两种方式实现数据读取
3. 记录时间

```
DECLARE
i INT;
BEGIN
i := 10;
WHILE(i<100000)
LOOP
    i := i+1;
    insert into XXX .....;
    COMMIT;
END LOOP;
END;
```

简单执行后，发现第一种方面执行时间在200s～300s之间，其中每一次读取数据的时间在60s左右，在内存中做关联的时间在70s左右；第二种方案耗时在60s左右。根据简单的测试可以看出每一次大数据量的查询耗时基本是稳定的，猜测花在网络传输的时延远超表关联所需的时间，需要进一步验证。在这种情况下，目前选择第二种方案。
总结：实验结果有点显而易见的感觉，在这个过程中尝试写了存储过程，并简单设计了实验方案，也算是迈出了自己去验证不确定问题的第一步。


