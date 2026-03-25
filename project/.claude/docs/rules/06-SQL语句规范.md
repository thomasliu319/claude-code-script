# 06-SQL语句规范

## 核心原则

所有与 SQL 相关的 DDL（数据定义语言）和 DML（数据操作语言）语句必须写在 **script init 项目**中，禁止放在业务代码中。

## 规范说明

### 禁止在业务代码中

- ❌ **禁止**在 `schedule-tasks` 项目中存放 `.sql` 文件
- ❌ **禁止**在 `src/main/resources` 或其他目录下包含 SQL 脚本
- ❌ **禁止**使用 SQL 字符串拼接执行 DDL 操作

### 必须在 script init 项目中

- ✅ 所有建表语句（DDL）必须放在 script init 项目
- ✅ 所有数据初始化脚本（DML）必须放在 script init 项目
- ✅ SQL 文件由 script init 项目统一管理和执行

## 示例

### 错误示例

```bash
# ❌ 错误：在 schedule-tasks 项目中
schedule-tasks/
└── sql/
    └── food_scale_report_clickhouse.sql  # 禁止
```

### 正确示例

```bash
# ✅ 正确：在 script init 项目中
script-init/
└── sql/
    └── food_scale_report_clickhouse.sql  # 正确
```

## 注意事项

1. **建表语句迁移**：如发现业务代码中存在 SQL 文件，应立即迁移至 script init 项目
2. **版本管理**：SQL 脚本的版本控制和执行由 script init 项目负责
3. **跨项目协作**：业务代码需要依赖的数据结构由 script init 项目保证正确执行
