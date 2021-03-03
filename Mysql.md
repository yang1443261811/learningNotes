- 共享锁和排他锁也叫读锁和写锁, 写锁相比于读锁有更高的优先级, 因此一个写锁请求可能会插入到读锁队列的前面

- 锁的弊端, 加锁需要消耗资源, 锁的各种操作, 包括获得锁, 检查锁是否解除, 释放锁等, 都会增加系统的开销, 如果系统花费大量时间来管理锁, 而不是存取数据, 那么系统的性能可能会受此影响

- 表锁: 表锁是Mysql中最基本的锁, 并且是开销最小的锁, 它会锁定整张表, 一个用户在对表进行写操作( 插入, 更新, 删除 ) 前需要获得写锁, 这会阻塞其他用户对该表的所有读写操作, 只有在没有写锁的情况下, 其他的用户才能获得读锁, 读锁是互相不阻塞的

- 行级锁可以最大程度的支持并发处理 ( 同时也带来了最大的锁开销 )

- 事务是一组原子性的SQL查询, 如果数据库引擎能够成功地对数据库应用该组查询的全部语句, 那么就执行该组查询, 事务内的语句要么全部执行成功, 要么全部执行失败

- 隔离级别, SQL定义了四种隔离级别, 较低级别的隔离通常可以执行更高的并发

  | 未提交读                                                     | 提交读       | 可重复读                                                     | 可串行化                                                     |
  | ------------------------------------------------------------ | ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | 事务中的修改, 即使没有提交,对其它事务, 也都是可见的, 这称为脏读 | 默认隔离级别 | 该级别保证了在同一个事务中多次读取同样记录的结果是一致的, 但无法解决幻读的问题 | 最高隔离级别, 它强制事务串行化执行, 它会在每一行读取的数据上都加锁, 所以可能导致大量的超时和锁争用问题 |

- show table status like 'table_name' 命令查看数据表的相关信息

- MyISAM引擎最典型的性能问题是表锁问题, 如果发现所有的查询都长期处于 "Locked" 状态, 那么表锁可能就是最大的罪魁祸首

- show full processlist 命令查看线程级相关信息