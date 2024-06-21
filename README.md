#  Android资源混淆工具使用说明 #

## A fork of https://github.com/shwenzhang/AndResGuard, only bug fixs,no new features.




## Changes

#### 1.2.23

兼容AGP 7.4.x

#### 1.2.22.6

1. only support gradle 7.0+
2. sevenzip support  osx aarch

#### 1.2.23-SNAPSHOT (from 1.2.22.6 )

1. update sevenzip version to **21.07** (except windows)
2. add new arch linux-arm_32/ linux-aarch_64

### How to Use(refer [origin repo](https://github.com/shwenzhang/AndResGuard),and modify as belows)


### change group id:

com.tencent.mm --> io.github.leon406

### change version:
- **stable(mavenCentral):** 1.2.21 --> 1.2.23

- **snapshot:** 1.2.21 --> 1.2.22.6-SNAPSHOT

  ​	add snapshots repo to your build.gradle

```
maven {
    url "https://s01.oss.sonatype.org/content/repositories/snapshots/"
}
```



### 问题及临时解决方案

1. 无法进行混淆

   AGP 4.2.+ 引入资源压缩, 但效果不如AndResGuard,两个同时启用无法正常使用,需要在 gradle.properties禁用

   ```
   android.enableResourceOptimizations=false
   ```

   测试AGP 4.2.2 AGP 7.0.4 可以正常使用

2. 7zip无法运行

   配置本地[7zip](https://7-zip.org/)文件路径

   ```
   sevenzip {
           path = "xxxx/SevenZip-windows-x86_64.exe"
       }
   ```

3. 避免字体资源混淆 （API 级别 26引入字体资源）

   ```
   andResGuard {
   	whiteList = [
   	"R.font.*
   	]
   }
   ```

4. ConstraintLayout布局约束失效

   constraint_referenced_ids不能混淆,请用通配符加入白名单,如constraint_xxx

   ```
   andResGuard {
   	whiteList = [
   	"R.id.constraint*
   	]
   }
   ```

5. 已测试AGP版本

   - 7.0.4
   - [7.1.1](https://www.jianshu.com/p/60df0c03bbf3) 有兼容问题
   - 7.3.1
   - 7.4.1  (1.2.23+ 支持)
   - 8.x 不支持 (jdk版本升级17,功能无法正常使用, 建议使用低版本jdk +命令行进行混淆), 可以使用([lalakii的AGP 8.x版本](https://github.com/lalakii/AndResGuard))  

   
