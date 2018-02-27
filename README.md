# antd-dev-guide

公司内部维护ant-design版本使用

## 开发环境

### clone项目

项目地址：https://github.com/sunny-lab/ant-design

```shell
git clone https://github.com/sunny-lab/ant-design.git
```

### 开始编译

antd的组件，通过[Bi Sheng](https://github.com/benjycui/bisheng)这个开源项目创建的官网来展现。

在项目根目录下运行以下命令，可以启动开发环境，所有对源码（包括官网源码）的改动都会实时编译：

```shell
npm start
```

## 组件编写

在 components 文件夹下新建一个文件夹并以组件的名字命名，目录结构如下：

```
- myComponent
--- demo //代码演示
----- *.md
--- style
----- *.less
----- index.tsx //样式的入口文件
--- index.tsx //组件的入口文件
--- index.zh-CN.md //文档的入口文件
```

组件编写完成后在 components/index.tsx 文件里边把新加的组件 import 进来就可以了。

## 文档编写

### 文档入口文件格式

```markdown
---
category: Components
subtitle: 卡片
type: Data Display
title: Card
---

卡片。

## 何时使用

最基础的卡片容器，可承载文字、列表、图片、段落，常用于后台概览页面。

## API

| 参数 | 说明 | 类型 | 默认值 |
| --- | --- | --- | --- |
```

### 代码演示文件格式

在 demo 文件夹下创建一个 markdown 文件，名字任意。然后以如下格式编写，每个 demo 单独一个文件。

```markdown
---
order: 1
title:
  zh-CN: 普通卡片
  en-US: Normal Card
---

## zh-CN

包含标题、内容、操作区域。


//````jsx
import { Card } from 'antd';

class Container extends React.Component {
  render() {
    return <Card title="标题" extra={<a>more</a>}>测试内容</Card>
  }
}

ReactDOM.render(<Container />, mountNode);
//````
```

## 版本发布
