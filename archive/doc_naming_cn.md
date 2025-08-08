# 文档生成模板指南

## 文档命名模板

### 命名格式
```
{TYPE}_v{VERSION}_{TIMESTAMP}.md
```

### 参数说明

**{TYPE}**: 文档类型缩写
- `sdd`: 系统设计文档 (System Design Document)
- `api`: API文档 (API Documentation)
- `req`: 需求文档 (Requirements Document)
- `test`: 测试文档 (Test Documentation)
- `deploy`: 部署指南 (Deployment Guide)
- [自定义其他类型]

**{VERSION}**: 版本号 (v1, v2, v3...)

**{TIMESTAMP}**: 时间戳 (YYYYMMDDHHSS)
确保使用bash获取当前时间

### 命名示例
- `sdd_v1_202507131900.md` (系统设计文档)
- `api_v2_202507140930.md` (API文档)
- `req_v1_202507121500.md` (需求文档)

**规则**
将生成的文档保存到项目内的 **doc/** 文件夹

### 使用方法

#### 基础用法
```
@your_project/prompt/doc_naming_template.md
TYPE = 'sdd'        # 文档类型
VERSION = '1'       # 版本号
PROJECT_NAME = '你的项目名称'
```