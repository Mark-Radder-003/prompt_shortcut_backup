🌐 **Languages:** [English](README.md) | [日本語](README_ja.md)

## 🚀 Quick Start

### Using Templates in Your Project

#### Create Symbolic Link (Recommended)

**Why Symbolic Links?**
- **📁 Single Source of Truth**: Maintain templates in one central location
- **🔄 Automatic Updates**: All projects instantly get template improvements
- **🚫 No Duplication**: Avoid managing multiple copies across projects
- **✅ Version Consistency**: Ensure all projects use the same template version

**Use Case Example:**
Imagine you have 10 projects all using the same prompt templates. Without symbolic links, you'd need to:
- Copy templates to all 10 projects (10x storage)
- Update all 10 copies when you improve a template (10x effort)
- Risk having different versions across projects (inconsistency)

With symbolic links, you:
- Maintain templates in ONE location
- Update once, all projects benefit immediately
- Guaranteed consistency across all projects

```bash
# Navigate to your project
cd ~/workspace/your-project

# Create symbolic link to main templates
ln -s ~/Documents/_prompt/main _prompt_alias

# Now you can reference templates using @_prompt/template_name.md
```

## Usage

Run this in Claude Code 👇
```
@_prompt/xxx_template.md

**Reference files for this template
```

### Sample
![usage_sample](usage_sample.png)