# Document Generation Template Guide

## Document Naming Template

### Naming Format
```
{TYPE}_v{VERSION}_{TIMESTAMP}.md
```

### Parameter Description

**{TYPE}**: Document type abbreviation
- `sdd`: System Design Document
- `api`: API Documentation  
- `req`: Requirements Document
- `test`: Test Documentation
- `deploy`: Deployment Guide
- [Custom other types]

**{VERSION}**: Version number (v1, v2, v3...)

**{TIMESTAMP}**: Timestamp (YYYYMMDDHHSS)

### Naming Examples
- `sdd_v1_202507131900.md` (System Design Document)
- `api_v2_202507140930.md` (API Documentation)
- `req_v1_202507121500.md` (Requirements Document)

**rule**
save Generated Document  to this folder **doc/** inside the prj

### Usage

#### Basic Usage
```
@your_project/prompt/doc_naming_template.md 
TYPE = 'sdd'        # Document type 
VERSION = '1'       # Version number 
PROJECT_NAME = 'Your Project Name'
```