>   **优乐选电商系统开发**

>   **第 5 章**

>   **商品录入【1】**

>   优就业.JAVA 教研室

课程目标
========

>   目标 1：完成商品分类功能

>   目标 2：了解电商概念 SPU 和 SKU 目标 3：掌握富文本编辑器的使用目标
>   4：掌握上传服务器 FastDFS 目标 5：掌握 angularJS 图片上传

1.  商品分类

    1.  需求及表结构分析

        1.  需求分析

>   实现三级商品分类列表查询功能

>   进入页面首先显示所以一级分类，效果如下：

![](media/afc79e6033b02c25f04e1dbbcc7c2cdf.jpg)

>   点击列表行的查询下级按钮，进入下级分类列表，同时更新面包屑导航

![](media/2c3b6100d8c26da36bded79cd1188031.jpg)

>   再次点击表行的查询下级按钮，进入三级分类列表，因为三级分类属于最后一级，所以在列
>   表中不显示查询下级按钮，同时更新面包屑导航

office365

![](media/8b18845aa33c49d50de7f3fb967d9273.jpg)

>   点击面包屑导航，可以进行返回操作。

### 表结构分析

#### tb_item_cat 商品分类表

| 字段      | 类型    | 长度 | 含义        |
|-----------|---------|------|-------------|
| id        | Bigint  |      | 主键        |
| parent_id | Bigint  |      | 上级 ID     |
| name      | varchar |      | 分类名称    |
| type_id   | Bigint  |      | 类型模板 ID |

1.  **列表实现**

    1.  **后端代码**

>   修改 youlexuan-sellergoods-interface 工程 ItemCatService 接口，新增方法定义

>   修改 youlexuan-sellergoods-service 工程 ItemCatServiceImpl ，实现方法

![](media/21963ae81ebba9a616366011d2f55a94.jpg)

>   修改 youlexuan-manager-web 的 ItemCatController.java

### 前端代码

1.  修改 itemCatService.js

![](media/21963ae81ebba9a616366011d2f55a94.jpg)

1.  修改 itemCatController.js

2.  修改 item_cat.html

>   引入 JS

>   指令定义

>   循环列表

![](media/21963ae81ebba9a616366011d2f55a94.jpg)

面包屑导航
----------

>   我们需要返回上级列表，需要通过点击面包屑来实现 修改 itemCatController.js

![](media/21963ae81ebba9a616366011d2f55a94.jpg)

>   修改列表的查询下级按钮，设定级别值后 显示列表

>   这里我们使用了 ng-if 指令，用于条件判断，当级别不等于 3
>   的时候才显示“查询下级”按钮

>   绑定面包屑：

![](media/21963ae81ebba9a616366011d2f55a94.jpg)

新增商品分类（学员实现）
------------------------

>   实现商品分类，如下图:

![](media/7e8e42f0ae6d7b832664d99c997dbd28.jpg)

>   当前显示的是哪一分类的列表，我们就将这个商品分类新增到这个分类下。

>   实现思路：我们需要一个变量去记住上级 ID，在保存的时候再根据这个 ID
>   来新增分类修改 itemCatController.js, 定义变量

>   查询时记录上级 ID

![](media/21963ae81ebba9a616366011d2f55a94.jpg)

>   保存的时候，用到此变量

![](media/21963ae81ebba9a616366011d2f55a94.jpg)

>   修改页面 item_cat.html

![](media/21963ae81ebba9a616366011d2f55a94.jpg)

1.  新增商品分类--实现模板下拉列表（学员实现）

    1.  后端代码

2.  、修改 youlexuan-dao 工程 TbTypeTemplateMapper
    接口，新增获取模板列表数据方法

3.  、修改 youlexuan-dao 工程 TbTypeTemplateMapper.xml ，新增获取模板列表配置

4.  、修改 youlexuan-sellergoods-interface 工程 TypeTemplateService
    接口，新增方法定义

5.  、修改 youlexuan-sellergoods-service 工程 TypeTemplateServiceImpl ，实现方法

![](media/21963ae81ebba9a616366011d2f55a94.jpg)

1.  、修改 youlexuan-manager-web 工程 TypeTemplateController，实现方法

    1.  前端代码

2.  、修改 youlexuan-manager-web 工程 typeTemplateService.js
    新增获取下拉菜单数据方法

3.  、修改 youlexuan-manager-web 工程 itemCatController.js
    新增获取下拉菜单数据方法

|   | \$scope | .typeTemplateList={data:[]};//模板列表 |
|---|---------|----------------------------------------|
|   |         |                                        |

![](media/21963ae81ebba9a616366011d2f55a94.jpg)

>   注意：需要在 itemCatController 引入 typeTemplateService

|                          | app | .controller('itemCatController' ,**function**(\$scope,\$controller,itemCatServi |
|--------------------------|-----|---------------------------------------------------------------------------------|
| ce,typeTemplateService){ |     |                                                                                 |

1.  、修改 youlexuan-manager-web 工程中的 item_cat.html，引入相关 js

![](media/21963ae81ebba9a616366011d2f55a94.jpg)

1.  、修改 youlexuan-manager-web 工程中的 item_cat.html，修改模板 id 为下拉选择

>   注意：这里数据绑定使用的是 *ng-model 绑定下拉菜单获取到的 id，但是
>   select2-model 必须要声明，不然会报错。*

1.  、在 body 增加页面初始化调用商品类型菜单数据

2.  、运行测试效果如下：

![](media/574b08697cd75cf05198c709d88c6c9c.jpg)

修改商品分类（学员实现）
------------------------

>   修改 item_cat.html 的修改按钮

| \< | button | type=*"button"* | class=*"btn* | *bg-olive* | *btn-xs"* | data-toggle=*"modal"* |
|----|--------|-----------------|--------------|------------|-----------|-----------------------|


![](media/21963ae81ebba9a616366011d2f55a94.jpg)

删除商品分类（学员实现）
------------------------

1.  修改 item_cat.html 的删除按钮

2.  修改 item_cat.html，类别单选框

3.  修改 itemCatController.js 的删除方法，删除后返回指定父 id 的类别

4.  电商概念及表结构分析

    1.  电商概念 SPU 与 SKU

#### SPU = Standard Product Unit （标准产品单位）

>   SPU
>   是商品信息聚合的最小单位，是一组可复用、易检索的标准化信息的集合，该集合描述了一个产品的特性。

>   通俗点讲，属性值、特性相同的商品就可以称为一个 SPU。

>   例如：

>   iphone7 就是一个 SPU，与商家，与颜色、款式、套餐都无关。

#### SKU=stock keeping unit(库存量单位)

>   SKU 即库存进出计量的单位， 可以是以件、盒、托盘等为单位。

>   SKU
>   是物理上不可分割的最小存货单元。在使用时要根据不同业态，不同管理模式来处理。在服装、鞋类商品中使用最多最普遍。

>   例如：

>   纺织品中一个 SKU 通常表示：规格、颜色、款式。

表结构分析
----------

>   Tb_goods 商品表

![](media/bef790fd54f6fbf4be7810877942abba.jpg)

![](media/ab10159b16eafccfd838383e9d685262.jpg)

>   Tb_goods_desc 商品扩展信息表

![](media/ed77c226e67cde0816dd6fdfbf867447.jpg)

>   Tb_item SKU 表

![](media/5076d07fdb98ef3c896f4c425bf9a4c7.jpg)

1.  商家后台-商品录入【基本功能】

    1.  需求分析

>   在商家后台实现商品录入功能。包括商品名称、副标题、价格、包装列表、售后服务

![](media/be8effa7774d954a6bd66239a0bc312b.jpg)

1.  后端代码

    1.  实体类

>   找到工程 youlexuan-pojo 在 com.offcn.group 包下，创建组合实体类 goods

![](media/21963ae81ebba9a616366011d2f55a94.jpg)

### 数据访问层

>   由于我们需要在商品表添加数据后可以得到自增的 ID,所以我们需要在
>   TbGoodsMapper.xml

>   中的 insert 配置中添加如下配置

| \<selectKey resultType=*"java.* | *lang.* | *Long"* order=*"AFTER"* keyProperty=*"id"*\> |
|---------------------------------|---------|----------------------------------------------|
| SELECT LAST_INSERT_ID() AS id   |         |                                              |

>   \</selectKey\>

### 服务接口层

>   修改 youlexuan-sellergoods-interface 的 GoodsService 接口 add 方法

![](media/21963ae81ebba9a616366011d2f55a94.jpg)

### 服务实现层

>   修改 youlexuan-sellergoods-service 的 GoodsServiceImpl.java

### 控制层

>   修改 youlexuan-shop-web 工程的 GoodsController 的 add 方法

![](media/21963ae81ebba9a616366011d2f55a94.jpg)

1.  前端代码

    1.  控制层

>   修改 goodsController.js
>   ，在增加成功后弹出提示，并清空实体（因为编辑页面无列表）

![](media/21963ae81ebba9a616366011d2f55a94.jpg)

### 页面

>   修改 goods_edit.html

>   引入 JS:

>   定义控制器：

>   表单部分代码：

![](media/21963ae81ebba9a616366011d2f55a94.jpg)

>   \<input type=*"text"* class=*"form-control"
>   ng-model*=*"entity.goods.goodsName"* placeholder=*"商品名称"* value=*""*\>

>   \</div\>

>   \<div class=*"col-md-2 title"*\>副标题\</div\>

>   \<div class=*"col-md-10 data"*\>

>   \<input type=*"text"* class=*"form-control"
>   ng-model*=*"entity.goods.caption"* placeholder=*"副标题"* value=*""*\>

>   \</div\>

>   \<div class=*"col-md-2 title"*\>价格\</div\>

>   \<div class=*"col-md-10 data"*\>

>   \<div class=*"input-group"*\>

>   \<span class=*"input-group-addon"*\>¥\</span\>

>   \<input type=*"text"* class=*"form-control" ng-model*=*"entity.goods.price"*
>   placeholder=*"价格"* value=*""*\>

>   \</div\>

>   \</div\>

>   \<div class=*"col-md-2 title rowHeight2x"*\>包装列表\</div\>

>   \<div class=*"col-md-10 data rowHeight2x"*\>

>   \<textarea rows=*"4"* class=*"form-control"
>   ng-model*=*"entity.goodsDesc.packageList"*
>   placeholder=*"包装列表"*\>\</textarea\>

>   \</div\>

>   \<div class=*"col-md-2 title rowHeight2x"*\>售后服务\</div\>

>   \<div class=*"col-md-10 data rowHeight2x"*\>

>   \<textarea rows=*"4"* class=*"form-control"
>   ng-model*=*"entity.goodsDesc.saleService"*
>   placeholder=*"售后服务"*\>\</textarea\>

![](media/21963ae81ebba9a616366011d2f55a94.jpg)

>   保存按钮

1.  商家后台-商品录入【商品介绍】

    1.  需求分析

>   实现商品介绍的录入，要求使用**富文本编辑器**

![](media/8f2d5e1167d45b39933ede30672004eb.jpg)

富文本编辑器介绍
----------------

>   富文本编辑器，Rich Text Editor, 简称 RTE, 它提供类似于 Microsoft Word
>   的编辑功能。常用的富文本编辑器：

>   KindEditor http://kindeditor.net/

>   UEditor http://ueditor.baidu.com/website/ CKEditor http://ckeditor.com/

1.  使用 kindeditor 完成商品介绍的录入

    1.  导入 kindeditor 编辑器所需 js 类库

    2.  **初始化 kindeditor 编辑器**

>   在页面中添加 JS 代码，用于初始化 kindeditor

>   allowFileManager 【是否允许浏览服务器已上传文件】 默认值是：false

>   注意：编辑器对象名称是 editor，要不然会取不到值

### 提取 kindeditor 编辑器的内容

>   在 goodsController.js 中的 add()方法中添加

### 清空 kindeditor 编辑器的内容

>   修改 goodsController.js 的 add 方法

1.  分布式文件服务器 FastDFS

    1.  什么是 FastDFS

>   FastDFS 是用 c 语言编写的一款开源的分布式文件系统。FastDFS
>   为互联网量身定制，
>   充分考虑了冗余备份、负载均衡、线性扩容等机制，并注重高可用、高性能等指标，使用FastDFS
>   很容易搭建一套高性能的文件服务器集群提供文件上传、下载等服务。

>   FastDFS 架构包括 Tracker server 和 Storage server。客户端请求 Tracker server
>   进行文件上传、下载，通过 Tracker server 调度最终由 Storage server
>   完成文件上传和下载。

>   Tracker server 作用是负载均衡和调度，通过 Tracker server
>   在文件上传时可以根据一些策略找到 Storage server 提供文件上传服务。可以将
>   tracker 称为追踪服务器或调度服务器。

>   Storage server 作用是文件存储，客户端上传的文件最终存储在 Storage 服务器上，
>   Storageserver 没有实现自己的文件系统而是利用操作系统
>   的文件系统来管理文件。可以将storage 称为存储服务器。

![](media/ff8e0479f8095f4bd6e990d57e99b697.jpg)

>   服务端两个角色：

>   Tracker：管理集群，tracker 也可以实现集群。每个 tracker 节点地位平等。收集
>   Storage

>   集群的状态。

>   Storage：实际保存文件 Storage
>   分为多个组，每个组之间保存的文件是不同的。每个组内部可以有多个成员，组成员内部保存的内容是一样的，组成员的地位是一致的，没有
>   主从的概念。

1.  文件上传及下载的流程

    1.  文件上传流程

![](media/27343afe306112d9e10d1a2cdfa62936.jpg)

>   客户端上传文件后存储服务器将文件 ID 返回给客户端，此文件 ID
>   用于以后访问该文件的索引信息。文件索引信息包括：组名，虚拟磁盘路径，数据两级目录，文件名。

![](media/b871b97cbe96fbe4a6b7eb1e1c14e121.jpg)

>   **组名**：文件上传后所在的 storage 组名称，在文件上传成功后有 storage
>   服务器返回， 需要客户端自行保存。

>   **虚拟磁盘路径**：storage 配置的虚拟路径，与磁盘选项
>   store_path\*对应。如果配置了store_path0 则是 M00，如果配置了 store_path1
>   则是 M01，以此类推。

>   **数据两级目录**：storage
>   服务器在每个虚拟磁盘路径下创建的两级目录，用于存储数据文件。

>   **文件名**：与文件上传时不同。是由存储服务器根据特定信息生成，文件名包含：源存储
>   服务器 IP 地址、文件创建时间戳、文件大小、随机数和文件拓展名等信息。

### 文件下载流程

![](media/8af18262528902373b4bf31160f13820.jpg)

1.  **最简单的 FastDFS 架构**

![](media/c3dab4f35439d09dc566bba2ad30fd9e.jpg)

1.  **FastDFS 安装**

>   FastDFS
>   安装步骤非常繁琐，我们在课程中不做要求。已经提供单独的（\\资源\\配套软件

>   \\fastDFS\\FastDFS 安装部署文档）供学员们课后阅读。

>   为了能够快速的搭建 FastDFS
>   环境进行代码开发，我们这里提供了安装好的镜像。解压“资源/Linux
>   镜像/fastDFS/FastDFS.rar”,双击 vmx 文件，然后启动。

>   注意：遇到下列提示选择“我已**移动**该虚拟机”！

![](media/2c6a41a5f8de18f1d7674638b0129d53.jpg)

>   IP 地址已经固定为 **192.168.188.146** ，请设置你的虚拟机 NAT 主机网段为
>   188。登录名为 root 密码为 offcn123

FastDFS 入门小 Demo
-------------------

>   需求：将本地图片上传至图片服务器，再控制台打印 url

1.  创建 Maven 工程 fastDFSdemo pom.xml 中引入

2.  添加配置文件 fdfs_client.conf ，将其中的服务器地址设置为 192.168.188.146

3.  创建 java 类 TestStorageClient，代码如下：

![](media/21963ae81ebba9a616366011d2f55a94.jpg)

>   **package** fastDFSdemo;

>   **import** java.io.IOException;

>   **import** org.csource.common.MyException; **import**
>   org.csource.fastdfs.ClientGlobal; **import**
>   org.csource.fastdfs.StorageClient; **import**
>   org.csource.fastdfs.StorageServer; **import**
>   org.csource.fastdfs.TrackerClient;

>   **import** org.csource.fastdfs.TrackerServer;

>   **public class** TestStorageClient {

>   **public static void** main(String[] args) **throws** IOException,
>   MyException {

>   // 1、加载配置文件，配置文件中的内容就是 tracker 服务的地址。

>   ClientGlobal.*init*("./src/main/resources/fdfs_client.conf");

>   // 2、创建一个 TrackerClient 对象。直接 new 一个。

>   TrackerClient trackerClient = **new** TrackerClient();

>   // 3、使用 TrackerClient 对象创建连接，获得一个 TrackerServer 对象。

>   trackerServer = trackerClient.getConnection();

>   // 4、创建一个 StorageServer 的引用，值为 null StorageServer storageServer =
>   **null**;

>   // 5、创建一个 StorageClient 对象，需要两个参数 TrackerServer 对象、

>   StorageServer 的引用

>   StorageClient storageClient = **new** StorageClient(trackerServer,
>   storageServer);

>   // 6、使用 StorageClient 对象上传图片。

![](media/21963ae81ebba9a616366011d2f55a94.jpg)

>   注意：如果出现连接图片服务器超时失败的情况，请检查图片 linux
>   服务器是否启动、是否开启了端口 22122、23000
>   的防火墙端口，如果未开启需要开启。

>   控制台输出如下结果：

>   在浏览器输入：

>   <http://192.168.188.146/group1/M00/00/00/wKi8klv9PcCAN3w9AACSXEWdWYM543.jpg>

>   即可看到所上传的图片。

![](media/21963ae81ebba9a616366011d2f55a94.jpg)

1.  商家后台-商品录入【商品图片上传】

    1.  需求分析

>   在商品录入界面实现多图片上传

![](media/43eb4548352941ead8affcd9c304f6fc.jpg)

>   当用户点击新建按钮，弹出上传窗口

![](media/d2ef8b29c73350b9d0e7a198562d9549.jpg)

1.  后端代码

    1.  工具类

2.  youlexuan-common 工程 pom.xml 引入依赖

![](media/21963ae81ebba9a616366011d2f55a94.jpg)

1.  将“资源/fastDFS/工具类”的 FastDFSClient.java 拷贝到 youlexuan-common 工程

![](media/bad23ebe562e1272b4802f2286dc0fdf.jpg)

### 配置文件

1.  将“资源/fastDFS/配置文件”文件夹中的 fdfs_client.conf 拷贝到
    youlexuan-shop-web

>   工程 config 文件夹

1.  在 youlexuan-shop-web 工程 application.properties 添加配置

2.  在 youlexuan-shop-web 工程 springmvc.xml 添加配置：

![](media/21963ae81ebba9a616366011d2f55a94.jpg)

>   注意，一定要加载属性文件，要 不然在 Controler 里面没办法使用\@Value
>   引用属性值

### 控制层

>   在 youlexuan-shop-web 新建 UploadController.java

![](media/21963ae81ebba9a616366011d2f55a94.jpg)

>   \*

>   \*/ \@RestController

>   **public class** UploadController {

>   \@Value("\${FILE_SERVER_URL}")

>   **private** String FILE_SERVER_URL;//文件服务器地址

>   \@RequestMapping("/upload")

>   **public** Result upload( MultipartFile file){

>   //1、取文件的扩展名

>   String originalFilename = file.getOriginalFilename(); String extName =

>   originalFilename.substring(originalFilename.lastIndexOf(".") + 1);

>   **try** {

>   //2、创建一个 FastDFS 的客户端

>   FastDFSClient fastDFSClient = **new**

>   FastDFSClient("classpath:config/fdfs_client.conf");

>   //3、执行上传处理

>   String path = fastDFSClient.uploadFile(file.getBytes(), extName);

>   //4、拼接返回的 *url* 和 *ip* 地址，拼装成完整的 *url*

>   String url = FILE_SERVER_URL + path;

>   **return new** Result(**true**,url);

>   } **catch** (Exception e) {

![](media/21963ae81ebba9a616366011d2f55a94.jpg)

1.  前端代码

    1.  服务层

2.  在 youlexuan-shop-web 工程创建 uploadService.js

![](media/21963ae81ebba9a616366011d2f55a94.jpg)

>   anjularjs 对于 post 和 get 请求默认的 Content-Type header 是
>   application/json。通过设置‘Content-Type’: undefined，这样浏览器会帮我们把
>   Content-Type 设置为 multipart/form-data.

>   通过设置 transformRequest: angular.identity ，anjularjs transformRequest
>   function 将序列化我们的 formdata object.

1.  将 uploadService 服务注入到 goodsController 中

2.  在 goods_edit.html 引入 js

![](media/21963ae81ebba9a616366011d2f55a94.jpg)

### 上传图片

1.  goodsController 编写代码

![](media/21963ae81ebba9a616366011d2f55a94.jpg)

1.  修改图片上传窗口，调用上传方法，回显上传图片

![](media/21963ae81ebba9a616366011d2f55a94.jpg)

1.  修改新建按钮

![](media/21963ae81ebba9a616366011d2f55a94.jpg)

### 图片列表

1.  在 goodsController.js 增加方法

2.  修改上传窗口的保存按钮

3.  遍历图片列表

>   注意图片属性采用了 ng-src，可以保证有属性值的时候在加载图片，避免出现 404
>   错误

### 移除图片

>   在 goodsController.js 增加代码

![](media/21963ae81ebba9a616366011d2f55a94.jpg)

>   修改列表中的删除按钮
