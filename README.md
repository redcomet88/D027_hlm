# D027  vue+django+neo4j 基于知识图谱红楼梦问答系统

> 完整项目收费，可联系QQ: 81040295 微信: mmdsj186011 注明从github来的，谢谢！
也可以关注我的B站： 麦麦大数据 https://space.bilibili.com/1583208775
> 

编号：D027 
架构： vue+django+neo4j+mysql
## 视频


[video(video-1GsGdt4D-1761090823402)(type-bilibili)(url-https://player.bilibili.com/player.html?aid=115412113232550)(image-https://i-blog.csdnimg.cn/img_convert/6114509ce96e33c1929d22c30804fff9.jpeg)(title-D027 vue+django+neo4j 基于知识图谱红楼梦问答系统)]

## 项目背景

知识图谱是一种以图谱形式描述客观世界中存在的各种实体、概念及其关系的技术,  广泛应用于智能搜索、自动问答和决策支持等领域.  可视分析技术可以将抽象的知识图谱映射为图形元素,  帮助用户直观地感知和分析数据,  从而提高知识图谱的构建和表达,  也为知识图谱在各个领域的应用提供了有力支持。
知识图谱技术包括知识表示、知识图谱构建和知识图谱应用 3 方面的研究内容。  其中,  知识表示研究客观世界知识的建模,该过程需要用户设计合适的方法建模知识以方便机器识别和理解;
基于红楼梦人物关系的知识图谱问答系统首先整理了红楼梦的人物关系三元组数据，然后利用LTP技术进行问答系统的构建。
本系统是一个基于Vue+Django+Neo4j构建的红楼梦问答与知识图谱可视化系统，其核心功能围绕红楼梦知识的展示、问答和用户管理展开。主要包括：系统首页，用于展示系统概览和红楼梦相关背景信息；知识图谱模块，通过关系图谱可视化展示红楼梦人物间的关系，并支持查询功能；问答系统，支持用户通过自然语言提问，系统通过分词和词性标注分析，结合Neo4j数据库进行智能匹配，快速返回准确答案；仿真聊天功能，提供接近真人对话的交互体验，增强用户的使用乐趣；以及用户管理模块，包含登录、注册、实名认证、短信验证码修改密码等功能，为用户提供安全且个性化的使用体验
## 架构
该系统采用典型的B/S（浏览器/服务器）架构模式。用户通过浏览器访问Vue前端界面，前端由HTML、CSS、JavaScript以及Vue.js生态系统中的Vuex（用于状态管理）、Vue Router（用于路由导航）和Echarts（用于知识图谱可视化）等组件构建。前端通过API请求与Django后端进行数据交互，Django后端负责业务逻辑处理，并通过Py2Neo或其他适配工具与Neo4j图数据库进行交互，完成数据的存储和查询。此外，系统还实现了基于LTP模型的自然语言处理功能，用于问答系统的分词、词性标注和语义理解， 以及通过短信服务提供验证码，支持用户密码修改和实名认证等功能。
### 架构图
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/994ae188eb50462da0d6eb783f4a92f7.png)
## 实现功能
### 功能模块图
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/bd955dca6b6d40e1a63eb8c9751f7cd8.png)
### 1. 红楼梦人物关系的Neo4j导入；
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/18541124f61841959f22810b7caac11f.png)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/5a7976079995449b9b047be687eb8615.png)
### 2. vue+django的前后端分离系统构建；
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/438528b19f854c4995e7f588ea80fde5.png)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/6fc2e7358fd9428781eb4eacddbf8cc5.png)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/2ddd13209a2442c1937b63850e0a1afe.png)
### 3. 关系图谱Echarts 的展示和查询；
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/86718331555843ce996352da2cd85088.png)
### 4. 知识问答功能，通过分词与词性标注结果查询neo4j匹配答案，并且在前端展示结果；
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/2f7007dfbe5d46c18c725b717478808b.png)
### 5. 高度仿真的聊天界面，接近真人在线聊天；
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/be462ee5da5b4854a2c10c2ac9f9b34d.png)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/a2a18d4247f2437b903a17c876369795.png)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/64990bd8a52b4c5b8a39a00226b2c315.png)
### 6. 修改用户信息、短息验证码修改密码，实名认证等小创新点，同时支持登录与注册。
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/5e2c620af8f7426e87bb270a88157e73.png)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/2dca0b3103924364beddbd44fefc54fd.png)

```jsx
match(p)-[r:%s{relation: '%s'}]->(n:Person{Name:'%s'}) return  p.Name,n.Name,r.relation,p.cate,n.cate
match(p)-[r:父亲{relation: '父亲'}]->(n:Person{Name:'贾宝玉'}) return  p.Name,n.Name,r.relation,p.cate,n.cate

```

知识图谱是一种以图谱形式描述客观世界中存在的各种实体、概念及其关系的技术,  广泛应用于智能搜索、
自动问答和决策支持等领域.  可视分析技术可以将抽象的知识图谱映射为图形元素,  帮助用户直观地感知和分析数
据,  从而提高知识图谱的构建和表达,  也为知识图谱在各个领域的应用提供了有力支持.

## 代码说明
该功能实现了一个基于知识图谱的问答系统，专注于《红楼梦》人物关系的识别与回答。用户输入问题后，系统通过LTP进行分词和词性标注，识别出问题中的核心人物和关系词。随后，系统构建Cypher查询语句，查询Neo4j知识库中的相关关系数据，并将结果以友好的方式展示给用户。
代码实现了以下关键步骤：
使用LTP进行分词和词性标注，识别出问题中的目标人物和关系词。
根据识别的实体和关系构建Cypher查询语句，查询Neo4j知识库。
解析查询结果并生成用户友好的回答。
### 流程图
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/63f398a6453e411896be6e952b18045c.png)

### 核心代码
```python
import ltp
from py2neo import Graph

# 初始化LTP模型
ltp_model = ltp.LTP()

# 连接Neo4j数据库
graph = Graph("bolt://localhost:7687", auth=("neo4j", "password"))

def process_question(question):
    # 分词和词性标注
    segs, _ = ltp_model.seg([question])
    pos = ltp_model.pos(segs)
    
    # 提取人物和关系词
    target_persons = []
    relations = []
    for i in range(len(pos[0])):
        if pos[0][i] == 'nh':  # 人名
            target_persons.append(segs[0][i])
        elif pos[0][i] == 'v':  # 动词，可能表示关系
            relations.append(segs[0][i])
    
    # 构建Cypher查询
    query = "MATCH (p1:Person {name: $name1})-[:RELATION]-(p2:Person) RETURN p1, RELATION, p2"
    
    # 执行查询并返回结果
    result = graph.run(query, name1=target_persons[0])
    return result

# 示例使用
question = "林黛玉和谁有关系？"
result = process_question(question)
for record in result:
    print(f"林黛玉与{record['p2']['name']}有{record['RELATION']['name']}关系")

```
