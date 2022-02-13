1, 建立一个 S3
2，上传 lession25sg.yml 并且得到一个 url
3, 在cloudformation 那里 create stack, 然后在创建的过程中把 url 输入


删除的时候，只需要删除根堆栈就可以了，嵌入的也会被顺带删除

### 建立S3存储桶，上传安全组模版

+ S3
  - Name: deeplearnaws-cf-tpl

### 浏览器部署确认

+ 堆栈名称: lesson25
