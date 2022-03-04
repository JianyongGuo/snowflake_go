# snowflake_go
分布式唯一ID生成器, snowflake golang 版本的实现

# 用法
```
import snowflake
int63_abc := snowflake.NewID63()
```

# 各公司适配
```
说明:
1. 代码不做任何改动也可以使用, 使用的机器名做hash, 服务实例太多时冲突概率变大
2. 为了更好适配本公司的业务, 可以修改如下函数 getWorkerId_1024(), 该函数作用是获取服务实例号ID, 
   比如你们公司机器名是  some_module_cn01.123.docker, 这个函数就是获取结果是123

// 最多支持1024个实例
func getInstanceId() int64 {
   // some_module_cn01.123.docker 
   // 写自己的代码, 想办法截取机器名里的实例号, 
   // 返回结果应该是 int64(123)
}
```

# 特点 
1. 基本保证单调递增顺序 (仅时钟回拨时保证不了)
2. 支持时钟回拨
3. 一个服务最多支持1024个实例
4. 数字是 int63，有符号整数，转换为字符串最长是19位
5. 并发安全
6. 纯本地操作, 无网络IO


