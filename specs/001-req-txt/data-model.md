# 数据模型：项目管理平台

## 实体关系图

```
[用户] 1 ---< [项目] >---< [任务] >---< [评论]
[看板] 1 ---< [项目]
[任务状态] <--- [任务]
```

## 实体详细信息

### 用户 (User)
**描述**: 代表具有角色的团队成员

**属性**:
- id (string): 唯一标识符 (UUID)
- name (string): 用户姓名
- role (enum): 用户角色 (PRODUCT_MANAGER, ENGINEER)
- createdAt (datetime): 创建时间

**验证规则**:
- name: 非空，最大长度50个字符
- role: 必须是预定义的角色之一

### 项目 (Project)
**描述**: 代表具有名称和描述的工作计划

**属性**:
- id (string): 唯一标识符 (UUID)
- name (string): 项目名称
- description (string): 项目描述
- createdAt (datetime): 创建时间
- updatedAt (datetime): 最后更新时间

**验证规则**:
- name: 非空，最大长度100个字符
- description: 可选，最大长度500个字符

**关系**:
- 与用户: 多对多关系（项目可以有多个成员）
- 与任务: 一对多关系（项目包含多个任务）

### 任务 (Task)
**描述**: 代表具有标题、描述、状态和负责人的工作单元

**属性**:
- id (string): 唯一标识符 (UUID)
- title (string): 任务标题
- description (string): 任务描述
- status (enum): 任务状态 (TODO, IN_PROGRESS, REVIEW, DONE)
- assigneeId (string): 负责人ID（引用用户）
- projectId (string): 所属项目ID（引用项目）
- createdAt (datetime): 创建时间
- updatedAt (datetime): 最后更新时间

**验证规则**:
- title: 非空，最大长度200个字符
- description: 可选，最大长度1000个字符
- status: 必须是预定义的状态之一
- assigneeId: 可选，如果提供则必须引用有效的用户

**状态转换**:
- TODO → IN_PROGRESS: 开始任务
- IN_PROGRESS → REVIEW: 提交审核
- REVIEW → DONE: 完成任务
- REVIEW → IN_PROGRESS: 重新开始任务

**关系**:
- 与项目: 多对一关系（多个任务属于一个项目）
- 与用户: 多对一关系（任务分配给一个用户）
- 与评论: 一对多关系（任务可以有多个评论）

### 评论 (Comment)
**描述**: 代表任务上的注释或反馈

**属性**:
- id (string): 唯一标识符 (UUID)
- content (string): 评论内容
- authorId (string): 作者ID（引用用户）
- taskId (string): 所属任务ID（引用任务）
- createdAt (datetime): 创建时间
- updatedAt (datetime): 最后更新时间

**验证规则**:
- content: 非空，最大长度1000个字符
- authorId: 必须引用有效的用户
- taskId: 必须引用有效的任务

**关系**:
- 与任务: 多对一关系（多个评论属于一个任务）
- 与用户: 多对一关系（评论由一个用户创建）

### 看板 (KanbanBoard)
**描述**: 代表项目的任务可视化，具有不同状态的列

**属性**:
- id (string): 唯一标识符 (UUID)
- projectId (string): 所属项目ID（引用项目）
- columns (array): 列定义数组
- createdAt (datetime): 创建时间
- updatedAt (datetime): 最后更新时间

**列定义**:
- id (string): 列唯一标识符
- name (string): 列名称 (TODO, IN_PROGRESS, REVIEW, DONE)
- order (number): 列顺序

**关系**:
- 与项目: 一对一关系（一个看板对应一个项目）

## 索引策略

### 主键索引
- 所有实体的id字段都是主键

### 外键索引
- Task.projectId: 用于快速查找项目中的所有任务
- Task.assigneeId: 用于快速查找分配给用户的所有任务
- Comment.taskId: 用于快速查找任务的所有评论
- Comment.authorId: 用于快速查找用户创建的所有评论

### 复合索引
- Task.projectId + Task.status: 用于快速查找项目中特定状态的所有任务