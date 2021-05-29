# opensearch-analysis-hanlp
HanLP Analyzer for Opensearch  
此分词器基于[HanLP](http://www.hankcs.com/nlp)，提供了HanLP中大部分的分词方式。

> fork form https://github.com/KennFalcon/elasticsearch-analysis-hanlp

----------

版本对应
----------

| Plugin version | Branch version  |
| :------------- | :-------------- |
| 1.0.0            | 1.0.0 -> master             |

构建
----------
### 1. build with maven
```
mvn clean package
```

### 2. use build package at `target/releases/opensearch-analysis-hanlp-1.0.0.zip`

安装步骤
----------

### 1. 下载安装对应版本

```
./bin/elasticsearch-plugin install file://${PLUGIN_PATH}
```

### 2. 重启 Opensearch

### 3. 热更新

在本版本中，增加了词典热更新，修改步骤如下：

a. plugins/analysis-hanlp/data/dictionary/custom目录中新增自定义词典

b. 修改hanlp.properties，修改CustomDictionaryPath，增加自定义词典配置

c. 等待1分钟后，词典自动加载

**注：每个节点都需要做上述更改**

提供的分词方式说明
----------
- hanlp: hanlp默认分词
- hanlp_standard: 标准分词
- hanlp_index: 索引分词
- hanlp_nlp: NLP分词
- hanlp_crf: CRF分词
- hanlp_n_short: N-最短路分词
- hanlp_dijkstra: 最短路分词
- hanlp_speed: 极速词典分词

Notice
----------
如何为Opensearch重新编译该插件？
### 1. 将gradle项目转为maven项目，并移除gradle相关文件
> 由于目前opensearch缺少gradle构建所需的build-tools包，所以先转为maven项目再进行构建

在build.gradle中增加`apply plugin: 'maven'`语句，然后执行`./gradlew build`，成功后将在build/poms/目录下生成pom-default.xml文件，把它复制到根目录下，改名成pom.xml即可

### 2. 导入依赖包到idea中
- 在当前工程目录下新建lib目录，并拷贝所需的jar包到lib目录下
- 导入依赖包到idea中

### 3. 新增plugin-descriptor.properties文件

### 4. 修改pom.xml文件
- 增加依赖配置
- src/main下新增`assemblies/plugin.xml`文件，用于构建zip包
