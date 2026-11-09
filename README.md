# Quant Learning 量化学习：Python 数据栈五周实战

本仓库记录我为量化研究员岗位系统补齐 Python 数据栈的五周练习，
覆盖 NumPy、pandas、SQL、Linux 与 Git，全程命令行操作并保持每日提交。

## 运行环境

- 操作系统：Windows + WSL2 (Ubuntu)
- Python 3.12.5
- Git for Windows 2.56
- 核心依赖见 `requirements.txt`（numpy、pandas、matplotlib、seaborn、scipy、pyarrow、thefuzz 等）

## 目录结构

| 目录 | 内容 |
|---|---|
| `week1_numpy/` | NumPy 基础：ndarray、索引、轴、广播、ufunc、线性代数、随机数、蒙特卡洛 |
| `week2_pandas/` | pandas 基础：DataFrame、索引、清洗、字符串、条件函数、合并连接 |
| `week3_pandas_advanced/` | pandas 进阶：groupby、透视表、窗口函数、绘图、模糊匹配 |
| `week4_sql/` | SQL：查询、聚合、多表连接、子查询、窗口函数、pandas 衔接 |
| `linux_practice/` | Linux 命令与 shell 脚本练习 |
| `data/` | 数据文件（不入库，见下方数据说明） |

## 学习内容（按周）

### Week 1 · NumPy（D1–D7）
ndarray 构造与数据类型、花式/布尔索引、axis 轴运算、广播机制、
通用函数与聚合、线性代数、随机数生成器、蒙特卡洛方法。

### Week 2–3 · pandas（D8–D20）
DataFrame 读写与索引、缺失/重复/类型清洗、字符串方法、
concat 与 merge 四种连接、groupby 聚合、transform 与透视表、
rolling 窗口指标、对象式绘图、thefuzz 模糊匹配。

### Week 4 · SQL（D22–D28）
SELECT/WHERE/ORDER、聚合分组与 HAVING、多表 JOIN 与自连接、
子查询与 CASE、窗口函数（ROW_NUMBER/RANK/LAG/累计求和），
并完成 SQL 取数到 pandas 再可视化的衔接练习。

### Week 5 · Linux 与 Git（D29–D35）
WSL2 环境、文件操作、grep/find/管道、权限管理、进程控制、
环境变量、venv 虚拟环境、nohup/tmux 后台任务、ssh 远程，
以及 Git 本地提交、分支合并、冲突解决与 GitHub 远程协作。

## 关键成果

- 基于日线数据用 pandas 滚动窗口计算收益率、均线、波动率与动量，
  复权净值曲线终值 211.89，最大回撤 -81.71%。
- 完成 SQL 窗口函数分层查询与多表连接，理解 pandas 与 SQL 的口径对应。
- 在 GitHub 维护结构清晰、带完整提交历史的公开仓库。

## 数据说明

`data/` 目录已通过 `.gitignore` 忽略，不纳入版本库。
练习数据来自公开数据集（如 pandas_exercises、DAT8），
可通过其官方仓库或数据源重新下载。

## 后续规划

在数据栈基础上推进两个量化项目（A 股多因子选股、Avellaneda-Stoikov 做市模型），
并同步进行概率题与 LeetCode 训练，准备量化研究员暑期实习投递。
