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

所以需要注意的是，antd根目录下的`webpack.config.js`是属于`Bi Sheng`项目所要求的webpack规范

并且，antd使用了[antd-tools](https://github.com/ant-design/antd-tools)来构建工程，打包发布等流程结合了gulp+webpack功能，默认的webpack配置是包含在antd-tools的代码中的。

在常规开发中，不需要调整根目录下的`webpack.config.js`。

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

### 代码规范

每次编写组件后，需要使用`npm run lint`来检测是否符合代码规范。

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

### 自动化工具发布细节

antd项目发布前有一系列预处理和规范检测，基于[gulp task](https://github.com/ant-design/antd-tools/blob/master/lib/gulpfile.js)，自动化工具的具体流程如下：

1. check-git：检测是否有未提交的文件，保证git工作区的干净
2. dist：编译es2015代码为es5代码，并且进行压缩等操作
3. pre-publish：运行代码规范检测，运行测试代码
4. npm tag： 
5. tag：从package.json中读出版本号，执行git tag命令
6. github release![]()

### 发布流程

1. 确定所有的代码均已提交
2. 确定影响范围，是否有影响用户使用方式的改动，是否有严重的bug修复，均要添加在`CHANGELOG_SUNNY_LAB.md`中，为了方便跟进ant-design版本，不要修改ant-design本身的`CHANGELOG.md`
3. 修改`package.json`中的版本号，按照语义化进行修改
4. 提交本次修改
5. 在项目根目录下执行

    ```shell
    npm run pub
    ```
6. 发布网站，执行命令

   ```shell
   rm -rf node_modules && npm i
   npm run deploy
   ```


