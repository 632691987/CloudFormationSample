CloudFormation 模板结构
=======================

## 知识点

* 理解 CloudFormation 模板结构

## 官网

https://docs.aws.amazon.com/zh_cn/AWSCloudFormation/latest/UserGuide/template-anatomy.html

## 实战演习/说明讲解

+ 模版格式
+ 模版结构

## 操作步骤

### 模版格式

+ JSON
+ YAML(推荐)

### 模版结构

+ AWSTemplateFormatVersion
+ Description
+ Metadata
+ Parameters
+ Rules
+ Mappings
+ Conditions
+ Transform
+ Resources
+ Outputs

```yml
# Format Version（可选）模板符合的 AWS CloudFormation 模板版本。模板格式版本与 API 或 WSDL 版本不同。模板格式版本可独立于 API 和 WSDL 版本，进行独立更改。
AWSTemplateFormatVersion: "version date"

# Description (可选)一个描述模板的文本字符串。此部分必须始终紧随模板格式版本部分之后。
Description:
  String

# 元数据（可选）提供有关模板的其他信息的对象。
Metadata:
  template metadata

# Parameters（可选）要在运行时 (创建或更新堆栈时) 传递到模板的值。您可引用模板的 Resources 和 Outputs 部分中的参数。
Parameters:
  set of parameters

# 规则（可选）验证在堆栈创建或堆栈更新过程中传递给模板的参数或参数组合。
Rules:
  set of rules

# Mappings（可选）可用来指定条件参数值的密钥和关键值的映射，与查找表类似。可以通过使用 Resources 和 Outputs 部分中的 Fn::FindInMap 内部函数将键与相应的值匹配。
Mappings:
  set of mappings

# 条件（可选）用于控制是否创建某些资源或者是否在堆栈创建或更新过程中为某些资源属性分配值的条件。例如，您可以根据堆栈是用于生产环境还是用于测试环境来按照条件创建资源。
Conditions:
  set of conditions

# 转换 (可选) 对于无服务器应用程序（也称为“基于 Lambda 的应用程序”），指定要使用的 AWS Serverless Application Model (AWS SAM) 的版本。
Transform:
  set of transforms

# Resources（必需）指定堆栈资源及其属性，如 Amazon Elastic Compute Cloud 实例或 Amazon Simple Storage Service 存储桶。您可引用模板的 Resources 和 Outputs 部分中的资源。
Resources:
  set of resources

# Outputs（可选）描述在您查看堆栈的属性时返回的值。例如，您可以声明 S3 存储桶名称的输出，然后调用 aws cloudformation describe-stacks AWS CLI 命令来查看该名称。
Outputs:
  set of outputs
```







### CloudFormation 模版参数介绍

+ CF 模版运行时可以让用户指定模版的执行选项(参数)
  - EC2 实例类型，CIDR 范围等
+ 可以通过规则(Rule)校验用户的输入
+ 参数支持的类型
  - String
  - Number
  - List<Number> ("80,20")
  - CommaDelimitedList ("test,dev,prod")
  - AWS 特定的参数类型 (AWS::EC2::Image::Id, AWS::EC2::KeyPair::KeyName, List<AWS::EC2::VPC::Id>)
  - SSM 参数类型 (Parameter Store)
+ 模版中参数引用方式
  - Fn::Ref or !Ref
+ 其他常用属性
  - AllowedValues
  - Default
  - Description
  - MaxLength / MinLength
  - MaxValue / MinValue
  - NoEcho
    * 是否遮蔽参数值以防止在控制台、命令行或 API 中显示

### 参数的一般要求

+ 一个 AWS CloudFormation 模板中最多可包含 200 个参数。
+ 必须为每个参数提供一个逻辑名称 (也称为逻辑 ID)，该名称必须是字母数字，并且在模板内的所有逻辑名称中必须是唯一的。
+ 必须向每个参数分配一个受 AWS CloudFormation 支持的参数类型。
+ 必须向每个参数分配一个运行时的值，使 AWS CloudFormation 能够成功预置堆栈。您可以选择为要使用的 AWS CloudFormation 指定默认值，除非提供有其他值。
+ 必须在同一模板内声明和引用参数。您可以引用模板的 Resources 和 Outputs 部分中的参数。