###对表结构的说明
-----


####1.通知部分

#####1.1 material_owner
素材的索引信息
| 主键 |        名       |    类型   | 长度 | 非空 |            描述            |
|:----:|:---------------:|:---------:|:----:|:----:|:--------------------------:|
|   *  |   material_id   |    int    |  10  |   *  |           素材id           |
|      | material_sub_id |    int    |  11  |   *  |      素材所对应的主题      |
|      |      stu_id     |    int    |  11  |   *  |            学号            |
|      |  material_path  |  varchar  |  255 |   *  | 素材的相对路径（HTML形式） |
|      |  generate_time  | timestamp |      |   *  |         生成的时间         |
|      |     is_send     |  tinyint  |   4  |      |     是否被发送（发布）     |
|      |      title      |    char   |  64  |      |                            |

#####1.2 note_index
通知的索引信息
| 主键 |        名        |    类型   | 长度 | 非空 |                    描述                   |
|:----:|:----------------:|:---------:|:----:|:----:|:-----------------------------------------:|
|   *  |      note_id     |    int    |  10  |   *  |                   通知id                  |
|      |     note_sort    |  tinyint  |   4  |   *  |  通知的类型，0为通用型(管理员)，1为订阅型 |
|      |  publish_person  |    int    |  11  |   *  |                    学号                   |
|      |     is_passed    |  tinyint  |   4  |      |     审核是否通过（非管理员发布需审核）    |
|      |   publish_time   | timestamp |      |   *  |                 发送的时间                |
|      |    note_audit    |    int    |  11  |      |                   审核人                  |
|      |    note_topic    |    char   |  64  |      |                 通知的主题                |
|      | note_material_id |    int    |  11  |   *  |                内容的index                |
|      |  note_receivers  |    text   |      |   *  | 接收通知的人（实际上应该迁移到mongodb上） |

#####1.3 material_content(mongodb)
素材的内容信息
````
Schema:{
        __id:ObjectId,
        author: Number,(作者学号)
        id:Number,(对应mysql表中的material_id)
        topic_id:Number,
        classify:Boolean,(true为通用型，false为订阅型)
        tag:[String],(字符数组，标签)
        title:String，(标题）
        content:String(整个内容，百度富文本编辑器生成的内容，html)
        commmetn:[{author:String, content:String, good:Number}](评论)
    }
````
