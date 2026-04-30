# cc-api — Claude Code API Provider Switcher

管理多个 Claude API 提供商配置（API Key、Base URL、Model），在 Claude Code 中快速切换。

## 安装

确保 `~/.bashrc` 已添加以下内容（如已添加则跳过）：

```bash
export PATH="$PATH:/home/luowang/桌面/api_provider_Set"
```

重新加载配置：

```bash
source ~/.bashrc
```

## 配置

所有配置档案存储在 `~/.claude/api_profiles.ini`，格式如下：

```ini
[profile-name]
api_key = sk-your-key-here
base_url = https://api.example.com
model = claude-sonnet-4-6           # ANTHROPIC_MODEL，可选
tier = sonnet                       # 选中哪个 tier: opus/sonnet/haiku，可选
default_haiku = claude-haiku-4-5    # ANTHROPIC_DEFAULT_HAIKU_MODEL，可选
default_sonnet = claude-sonnet-4-6  # ANTHROPIC_DEFAULT_SONNET_MODEL，可选
default_opus = claude-opus-4-7      # ANTHROPIC_DEFAULT_OPUS_MODEL，可选
```

## 命令

| 命令 | 功能 |
|------|------|
| `cc-api list` | 列出所有配置，当前激活的标 `*` |
| `cc-api show` | 显示当前生效的完整配置 |
| `cc-api switch <name>` | 切换到指定配置（含 tier 模型） |
| `cc-api model <name>` | 仅切换 ANTHROPIC_MODEL |
| `cc-api model --clear` | 清除模型设置（使用提供商默认） |
| `cc-api tier <opus\|sonnet\|haiku>` | 仅切换 tier（不切换提供商） |
| `cc-api add <name>` | 添加新配置（交互式） |
| `cc-api remove <name>` | 删除配置 |
| `cc-api edit <name>` | 编辑配置文件 |

## 示例

```bash
# 查看所有配置
cc-api list

# 查看当前配置
cc-api show

# 切换提供商及模型
cc-api switch deepseek

# 仅切换模型
cc-api model claude-opus-4-7

# 仅切换 tier（不换 API Key/URL）
cc-api tier opus

# 添加新配置
cc-api add my-provider

# 删除配置
cc-api remove my-provider
```

## 字段说明

| INI 字段 | settings.json 目标 | 说明 |
|----------|-------------------|------|
| `api_key` | `env.ANTHROPIC_AUTH_TOKEN` | API 密钥 |
| `base_url` | `env.ANTHROPIC_BASE_URL` | API 端点 |
| `model` | `env.ANTHROPIC_MODEL` | 当前 tier 使用的模型 |
| `tier` | `model`（顶层） | Claude Code 的 tier 选择（opus/sonnet/haiku） |
| `default_haiku` | `env.ANTHROPIC_DEFAULT_HAIKU_MODEL` | Haiku tier 默认模型 |
| `default_sonnet` | `env.ANTHROPIC_DEFAULT_SONNET_MODEL` | Sonnet tier 默认模型 |
| `default_opus` | `env.ANTHROPIC_DEFAULT_OPUS_MODEL` | Opus tier 默认模型 |

## 文件

- **脚本**: `~/桌面/api_provider_Set/cc-api`
- **配置档案**: `~/.claude/api_profiles.ini`
- **Claude Code 配置**: `~/.claude/settings.json`
- **环境变量覆盖**: `CC_API_PROFILES` 和 `CC_API_SETTINGS` 可自定义配置和设置文件路径
