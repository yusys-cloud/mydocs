---
title: "Open Source Community"
date: 2023-05-18T11:20:59+08:00
# bookComments: false
# bookSearchExclude: false
---

## AI
- [ChatALL](https://github.com/sunner/ChatALL)同时与所有 AI 机器人聊天，找到最佳答案

## Workflow
[开源工作流引擎的精选列表](https://github.com/meirwah/awesome-workflow-engines)
### [flowy](https://github.com/alyssaxuu/flowy) 

The minimal javascript library to create flowcharts.

[flowy demo](http://flowy.yangzhiqiang.tech/)

### [dagu](https://github.com/dagu-dev/dagu)

Dagu 无代码工作流执行器。它根据声明性 YAML 定义执行工作流.是一个强大的 Cron 替代品，带有 Web UI。它允许您以声明性 YAML 格式将命令之间的依赖关系定义为有向无环图 (DAG)。此外，Dagu 原生支持运行 Docker 容器、发出 HTTP 请求以及通过 SSH 执行命令。

```shell
./dagu server
./dagu scheduler 
```

Usecase
- Data Pipeline Automation: Schedule ETL tasks for data processing and centralization.
- Infrastructure Monitoring: Periodically check infrastructure components with HTTP requests or SSH commands.
- Automated Reporting: Generate and send periodic reports via email.
- Batch Processing: Schedule batch jobs for tasks like data cleansing or model training.
- Task Dependency Management: Manage complex workflows with interdependent tasks.
- Microservices Orchestration: Define and manage dependencies between microservices.
- CI/CD Integration: Automate code deployment, testing, and environment updates.
- Alerting System: Create notifications based on specific triggers or conditions.
- Custom Task Automation: Define and schedule custom tasks using code snippets.

{{< tabs "uniqueid" >}}
{{< tab "MacOS" >}} MacOS Content {{< /tab >}}
{{< tab "Linux" >}} curl -LO  https://github.com/dagu-dev/dagu/releases/download/1.10.5/dagu_1.10.5_Linux_x86_64.tar.gz {{< /tab >}}
{{< tab "Windows" >}} Windows Content {{< /tab >}}
{{< /tabs >}}

[dagu demo](http://dagu.yangzhiqiang.tech/)

### 前端workflow
- https://github.com/BiaoChengLiu/easy-flow

