# Python 数据栈与工程基础 · 五周每日学习计划

> **周期**：2026-10-12（周一）～ 2026-11-15（周日），共 5 周 35 天
> **目标岗位**：国内量化机构 · 量化研究员实习
> **每日投入**：工作日 2.5–3 小时；周末 4–6 小时
> **本机环境**：Windows + Python 3.12.5 + VS Code；numpy 2.5.3、pandas 3.0.6
> **工作目录**：`D:\quant-learning\`，按周建子目录 `week1_numpy` … `week5_linux_git`

---

## 〇、使用说明

### 每日 3 小时时间模板

| 时段 | 时长 | 做什么 |
|---|---|---|
| ① | 30 min | 看书 / 官方文档，理解当天概念 |
| ② | 90 min | 跟着教程手敲代码（**禁止复制粘贴**） |
| ③ | 40 min | 合上资料，独立完成课后练习 |
| ④ | 20 min | 整理当天速查笔记，Git 提交 |

周末半天用于周复盘，半天做综合实战。

### 学习原则

1. **70% 时间动手敲代码**，看懂不等于会写。
2. 不背全部参数，目标是**高频 20% 的操作不查文档**，其余知道去哪查。
3. 报错先读最后一行，复制关键信息搜索——读报错是工程能力的一半。
4. 每天任务当天完成；欠账用周末补；**复盘日（D7/D14/D21/D28）不能跳过**。
5. 每个练习 notebook 顶部用 Markdown cell 写清：日期、主题、本次解决的问题。
6. 从 D8 起，每天结束前把代码提交 Git（第 2 周先用 VS Code 图形面板，第 5 周学命令行）。

### 核心资源清单

| 资源 | 用途 | 获取方式 |
|---|---|---|
| 《利用 Python 进行数据分析》第 3 版（Wes McKinney） | 主线参考书 | 微信读书 / 二手纸质；numpy/pandas 部分 |
| NumPy 官方 User Guide · Quickstart | numpy 查漏 | numpy.org/doc/stable/user/quickstart.html |
| pandas 官方文档（2.x/3.x） | pandas 查漏 | pandas.pydata.org/docs/ |
| `guipsamora/pandas_exercises` | pandas 题库 | GitHub 搜索仓库名，含全部数据 |
| Kaggle Learn（Pandas、Data Cleaning） | 免费微课 | kaggle.com/learn |
| 牛客网 · 题库「Python 数据分析」「SQL 篇」 | pandas / SQL 刷题 | nowcoder.com |
| SQLZOO | SQL 交互入门 | sqlzoo.net |
| LeetCode · 数据库题库 | SQL 收尾 | leetcode.cn |
| 《Linux 工具快速教程》`me115/linuxtools_rst` | Linux 中文速学 | GitHub |
| 廖雪峰 Git 教程 | Git 入门 | liaoxuefeng.com |

### ⚠️ 版本差异提醒（你的版本比教材新，以下以本计划写法为准）

- 随机数一律用新写法：`rng = np.random.default_rng(seed)`，不用 `np.random.rand`。
- pandas 逐元素处理：用 `DataFrame.map()`；教材里的 `applymap()` 已在 pandas 3.0 移除。
- 表拼接用 `pd.concat()`；`DataFrame.append()` 已移除。
- resample 频率别名更新：月末 `'ME'`（旧 `'M'`）、季末 `'QE'`、年末 `'YE'`、小时 `'h'`、分钟 `'min'`。
- 尽量用赋值式 `df = df.dropna()`，少依赖 `inplace=True`。
- 教材代码跑出 warning / error 时先对照本文件，解决不了就问。

---

## 环境准备（已于 D1 完成，留档备查）

- [x] 安装包：`pip install -i https://pypi.tuna.tsinghua.edu.cn/simple numpy pandas matplotlib seaborn jupyterlab ipykernel`
- [x] VS Code 打开 `D:\quant-learning`，内核选择 Python 3.12.5
- [x] 跑通 `day01_test.ipynb`：版本打印 + DataFrame + matplotlib 折线图
- [ ] **D7 前补做**：安装 Git for Windows（git-scm.com 下载，安装选项全部默认）；注册 GitHub 账号

---

# 第 1 周 · NumPy（10/12 – 10/18）

> 教材第 4 章 + NumPy Quickstart。本周产出：`week1_numpy/` 下 7 个 notebook + 1 份 `numpy_cheatsheet.md`。

## D1 · 10/12 周一｜ndarray 基础与数组创建 ✅ 已完成

**今日目标**：理解 ndarray 与 list 的本质区别，掌握 8 种创建方式与 4 个核心属性。

- [x] ndarray 概念：同质元素、连续内存、向量化；对比 `list*2`（重复）与 `array*2`（逐元素）
- [x] 创建：`np.array / zeros / ones / full / arange / linspace / eye`
- [x] 随机数：`default_rng(seed)` 的 `random / integers / normal`
- [x] 属性：`ndim / shape / size / dtype`；`astype` 类型转换
- [x] 一维 `(5,)` 与二维列向量 `(5,1)` 的区别
- [x] 练习 5 题（已批改通过）

## D2 · 10/13 周二｜索引、切片、布尔索引 ✅ 已完成

**今日目标**：掌握二维索引语法；理解视图/副本；熟练布尔筛选。

- [x] 一维切片：`a[1:4] / a[::2] / a[::-1]`
- [x] 二维索引：`m[0,1]`（推荐）、`m[:,1]`、`m[:2,:3]`；逗号前行后列
- [x] 视图与副本：切片是视图（共享内存），布尔/fancy 索引是副本；`.copy()` 与 `np.shares_memory`
- [x] 布尔索引：`x[x>0]`、`(x>0).sum()/mean()`；多条件 `& | ~`（**每条件加括号**）
- [x] `np.where(cond, x, y)` 与 `np.where(cond)`；fancy indexing `a[[4,0,2]]`
- [x] **订正**：练习 4 第三问改为 `(np.abs(d) > 1).sum()`（并集用 `|` 不是 `&`），补 `d[np.abs(d)>1]`

## D3 · 10/14 周三｜轴 axis、形状变换、广播（本周难点 ①）

**今日目标**：建立"轴"的直觉；背下广播规则并能预判任意两个数组能否运算。

**学习内容**
- 形状变换：`reshape`（元素数不变）、`ravel / flatten`、`squeeze / expand_dims`
- 拼接拆分：`concatenate(axis=)`、`vstack / hstack / stack`、`split`
- 转置：`.T`、`transpose`、`swapaxes`
- **axis 直觉**：`axis=0` 表示沿第 0 轴方向移动（跨行、把各行压到一起）→ 结果是"每列一个值"；`axis=1` 反之。用 `np.sum(m, axis=0)` 对照验证
- **广播三规则**（从右向左逐维对齐）：①维度数不同，在小的数组左侧补 1；②某维长度为 1，则沿该维复制；③长度既不相等又不为 1 → 报错
- 经典案例：`(3,)` 与 `(3,4)`；`(3,1)` 与 `(1,4)` → `(3,4)`（外积）；标量与任意数组

**课后练习**
1. 不运行先口算，再验证：`np.ones((3,4,5)).sum(axis=1).shape`、`np.zeros((2,3,4)).mean(axis=(0,2)).shape`
2. 把 `np.arange(12)` 分别 reshape 成 `(3,4)`、`(2,2,3)`、`(4,3)`，再展平。
3. 用 `(3,1)` 与 `(1,4)` 广播构造一个 3×4 矩阵，元素为行号与列号之和。
4. 给定 `m = rng.normal(0,1,(5,4))`，分别减去每列的均值、每行的均值（提示：`mean(axis=, keepdims=True)`）。
5. 制造一个广播报错的例子，并把错误信息最后一句抄下来。

## D4 · 10/15 周四｜ufunc、聚合、条件与排序

**今日目标**：掌握向量化数学运算、按轴聚合，以及量化排名常用的 argsort。

**学习内容**
- 逐元素函数：`+ - * / **`、`np.exp / log / sqrt / abs / round / floor / ceil / maximum / minimum`
- 聚合：`sum / prod / mean / median / var / std / min / max / argmin / argmax / percentile / quantile / any / all`；`axis`、`keepdims=True`
- 条件：`np.where`（三目）、`np.select([c1,c2],[v1,v2], default)`（多条件分级）、`np.clip(x, lo, hi)`
- 排序：`np.sort`（返回排序值）、`np.argsort`（返回排序索引——量化里做截面排名）、`np.partition`（了解）

**课后练习**
1. 造 6×4 随机矩阵：求每列最大值及其所在行号（`argmax(axis=0)`）。
2. 对每列做 min-max 归一化到 [0,1]（用 keepdims 保持形状）。
3. 用 `np.select` 把一组收益率分为：>0.02 为"大涨"、<−0.02 为"大跌"、其余"震荡"。
4. 用 `np.clip` 把正态样本限制在 [−2, 2]，验证超出部分被截断。
5. 给定分数数组，用 argsort 输出成绩从高到低的**原始下标**。

## D5 · 10/16 周五｜线性代数与随机数系统

**今日目标**：补齐矩阵运算 API；掌握常用分布抽样（蒙特卡洛的弹药库）。

**学习内容**
- 矩阵乘法：`A @ B`、`np.matmul`、`np.dot`（区分于逐元素 `*`）
- `np.linalg`：`inv / solve(A,b) / det / eig / qr / cholesky / norm`
- 统计相关：`np.cov`（协方差矩阵）、`np.corrcoef`（相关系数矩阵）
- Generator 抽样：`uniform / normal / standard_normal / integers / choice(p=, replace=) / permutation / shuffle`
- 分布：`binomial / poisson / exponential / lognormal / multivariate_normal(mean, cov)`

**课后练习**
1. 随机生成一个 4×4 对称正定矩阵（提示：`A = M.T @ M + I`），求逆并验证 `A @ inv(A) ≈ I`。
2. 用 `solve` 解线性方程组 Ax=b，与 `inv(A) @ b` 对比结果。
3. 用 `multivariate_normal` 抽 1000 个二维相关正态样本（相关系数 0.8），用 `corrcoef` 验证。
4. 用 `choice` 模拟掷骰子 10000 次（6 面等概率），统计各点数频率。
5. 用 `cumsum` 模拟一条 252 步的简单随机游走（每日 ±1）并画出路径。

## D6 · 10/17 周六｜蒙特卡洛综合实战（本周大练习，4–6 h）

**今日目标**：把 D1–D5 串成一个量化味道的完整实验，产出本周代表作。

**任务（notebook：`day06_monte_carlo.ipynb`）**
1. 模拟几何布朗运动（GBM）股价路径：S₀=100，μ=0.08，σ=0.25，T=1，252 个交易日，模拟 **10000 条**路径（二维数组，向量化，禁止双重 for）。
2. 画 3 张图：①前 50 条路径；②期末价格分布直方图 + 理论对数正态密度；③期末价格均值随路径数量（10²→10⁶）的收敛曲线（双对数坐标）。
3. 用蒙特卡洛给欧式看涨期权定价（K=100，r=0.03），再写 Black-Scholes 解析解，对比两者误差。
4. 分别用 for 循环版和向量化版各定价一次，`%timeit` 对比耗时，在 notebook 里记录倍数。
5. Markdown 结论：路径数量与定价误差的关系、向量化加速比、GBM 参数对结果的影响。

**自查**：10000×252 的数组内存占用是多少 MB？（float64 每元素 8 字节，自己算并与 `.nbytes` 对照）

## D7 · 10/18 周日｜复盘 + 速查笔记 + 装 Git

- [ ] 重做 D1–D5 全部错题与练习中当时没写出来的题
- [ ] 教材第 4 章通读扫漏，陌生 API 补进笔记
- [ ] 整理 `week1_numpy/numpy_cheatsheet.md`：创建 / 索引 / 形状 / 广播 / 聚合 / 随机数 六大块，每块只写函数名 + 一句话 + 最小示例
- [ ] **安装 Git for Windows**（git-scm.com，一路默认）；注册 GitHub 账号
- [ ] 自测：新建空白 notebook，不看笔记默写"造 5×3 正态矩阵 → 按列标准化 → 求每行最大值位置 → 按行和排序"全流程

---

# 第 2 周 · pandas 上（10/19 – 10/25）

> 教材第 5、6、7 章。产出：`week2_pandas/` 7 个 notebook + `pandas_cheatsheet_1.md`。
> 每天开始前先 `git pull`（本周先用 VS Code 左侧"源代码管理"面板点按钮提交）。

## D8 · 10/19 周一｜DataFrame 与文件读写

**今日目标**：创建/认识 DataFrame；熟练读写 CSV（实习第一天就干这个）。

**学习内容**
- Series：由 ndarray + index 构成；`.values / .index / .name`
- DataFrame 创建：dict of lists、二维数组 + columns/index、list of dicts
- 总览方法：`head/tail/info/describe/shape/columns/index/dtypes`
- `pd.read_csv` 核心参数：`sep, header, names, index_col, usecols, dtype, parse_dates, nrows, encoding, na_values`
- 写出：`to_csv(path, index=False)`、`to_excel`（需 `pip install openpyxl`）
- 直接从 URL 读 CSV（pandas 支持 http 路径）

**练习**
1. 用 dict 手写一个 10 只股票 × 字段（代码/行业/收盘价/市值）的 DataFrame。
2. 克隆 `guipsamora/pandas_exercises`（或下载 ZIP），读入 `Chipotle.tsv`（注意 `sep='\t'`）和 `chipo.csv`，用 info/describe 观察。
3. 只读取某 CSV 的指定 3 列（usecols），并把日期列解析为日期类型。
4. 把处理结果 `to_csv(index=False)` 写出，再读回来验证。

## D9 · 10/20 周二｜选择数据 + 缺失/重复/类型清洗

**今日目标**：掌握 loc/iloc；能独立清洗一份脏数据。

**学习内容**
- 选择：`df['col']`、`df[['c1','c2']]`、`df.loc[行标签, 列标签]`、`df.iloc[位置]`、`at/iat`
- 条件筛选：`df[df.age>20]`、多条件括号 + `&|~`、`df.query("age>20 and city=='BJ'")`
- 缺失：`isna()/notna()`、`isna().sum()` 统计、`fillna(值/均值/ffill/bfill)`、`dropna(how=, subset=, thresh=)`
- 重复：`duplicated()`、`drop_duplicates(subset=, keep=)`
- 类型：`astype`、`pd.to_numeric(errors='coerce')`、`rename(columns={})`、`replace`

**练习**
1. Chipotle：用 loc 取出 item_name 和 quantity 两列、第 3–8 行。
2. 造一个含缺失/重复/类型错误的 DataFrame（故意制造 5 类问题），逐类清洗并记录每步前后行数。
3. 把金额列里的 `$` 符号去掉并转 float（`str.replace` + `to_numeric`，为 D10 埋伏笔）。

## D10 · 10/21 周三｜字符串、排序、统计

**学习内容**
- `.str` 访问器：`contains / replace / split / strip / upper / startswith / len / extract（正则捕获组）`
- 排序：`sort_values(by=, ascending=, na_position=)`、`sort_index`、`nlargest / nsmallest`
- 统计：`value_counts(normalize=True, bins=)`、`unique / nunique / mode`、`count`
- 简单正则：`\d+`、`^`、`$`、`.*?`（够用即可，不系统学）

**练习**
1. Chipotle：清洗 item_price 为浮点；统计下单量 Top10 商品（value_counts / nlargest）。
2. 统计每个商品出现次数占比（normalize=True）。
3. 用 `str.extract` 从一段含数字编号的文本中提取编号。
4. Occupation 数据集：按年龄排序、统计各职业平均年龄。

## D11 · 10/22 周四｜map / apply 与新增列

**今日目标**：掌握按列变换和新增派生列（因子工程的基本动作）。

**学习内容**
- `Series.map({字典}) / map(函数)`：映射与逐元素变换
- `Series.apply / DataFrame.apply(axis=1)`：对行/列调用函数；`lambda`
- pandas 3.0：逐元素处理整个表用 `DataFrame.map()`（不是 applymap）
- 新增列：`df['new'] = ...`、`df.assign(a=..., b=...)`、`insert` 指定位置
- 条件造列：`np.where`、`np.select`（比 apply 快，优先用）
- 性能意识：内置向量化字符串/数值方法 > np.where > apply；apply 是最后手段

**练习**
1. 用字典 map 把行业代码映射为行业名称。
2. 用 `np.where` 新增"涨跌"列（收益率>0 为涨）；用 `np.select` 新增 5 档涨跌幅标签。
3. 写一个自定义函数（如：价格分档命名），分别用 map 和 apply 实现并计时对比。
4. World Food Facts 数据集：从产品名生成若干布尔特征列（含某关键词为 1）。

## D12 · 10/23 周五｜时间序列基础

**今日目标**：日期类型转换、按时间切片、重采样（日线→周线/月线）。

**学习内容**
- `pd.to_datetime`（format 参数加速、`errors='coerce'`）、Timestamp、DatetimeIndex
- `.dt` 访问器：`year/month/day/weekday/day_name/quarter/is_month_end`
- 时间索引：`set_index('date')` 后 `df.loc['2023':'2024-03']` 切片
- `resample('D'/'W'/'ME'/'QE'/'YE')` + 聚合（**pandas 3.0 用 ME/YE**）
- `DateOffset`、`to_period('M')` 了解

**练习**
1. 读入 pandas_exercises 中 `09_Time_Series/Getting_Financial_Data/Apple_stock.csv`，把 Date 转日期并设为索引。
2. 按时间切片取 2010 年数据、2012-06 至 2013-06 数据。
3. 日线收盘价 resample 成周线（OHLC 分别聚合：open 取 first、close 取 last、high 取 max、low 取 min、volume 求和）。
4. resample 成月度均价并画图。

## D13 · 10/24 周六｜pandas_exercises 集中训练（4–6 h）

完成 `guipsamora/pandas_exercises` 以下 6 组，**先独立写 20 分钟再看答案**：

- [ ] `01_Getting_&_Knowing_Your_Data/Chipotle`
- [ ] `01_.../Occupation`
- [ ] `01_.../World_Food_Facts`（只做前 20 题，数据大注意 nrows）
- [ ] `02_Filtering_&_Sorting/Chipotle`
- [ ] `02_.../Euro12`
- [ ] `02_.../Fictional_Army`

每组完成后在 notebook 末尾用 Markdown 记录：用到的 3 个最不熟的函数。

## D14 · 10/25 周日｜复盘 + pandas 速查笔记（上）

- [ ] 教材第 5、6、7 章通读扫漏
- [ ] 整理 `pandas_cheatsheet_1.md`：创建/读写、选择、清洗、字符串、排序统计、map/apply、时间序列
- [ ] 重做 D9–D12 练习中卡住的题
- [ ] Git 提交本周全部 notebook（commit message 示例：`week2: pandas basics exercises`）

---

# 第 3 周 · pandas 下 + 绘图（10/26 – 11/01）

> 教材第 8、9、10 章，第 11 章选读。产出：`week3_pandas_advanced/` + 一份技术指标 notebook（因子项目预演）。

## D15 · 10/26 周一｜表连接 concat / merge

**今日目标**：掌握多表合并（与周四 SQL JOIN 对照学，事半功倍）。

**学习内容**
- `pd.concat([df1,df2], axis=0/1, ignore_index=, join=)`；纵向拼接与横向拼接
- `pd.merge(left, right, how='inner/left/right/outer', on=, left_on=, right_on=, suffixes=, indicator=)`
- `df.join(other, on=)`（按索引连接）
- 一对多、多对多连接后行数变化（先想清楚再写）
- 验证键是否唯一：`df.key.is_unique`、`value_counts`

**练习**
1. 造三张表：客户表、订单表、商品表，完成 inner/left/outer 各一次，记录每种连接后的行数。
2. 用 indicator 找出"有客户但没下过单"的记录。
3. Fictional Army / 练习库中找 1 个 merge 题完成。

## D16 · 10/27 周二｜groupby 核心（本周重点 ①）

**今日目标**：吃透 split-apply-combine 三步。

**学习内容**
- `df.groupby('col')` 的惰性（分组对象不产生结果，聚合才产生）
- 单列/多列分组、分组后选列：`df.groupby(['a','b'])['v'].mean()`
- 内置聚合：`agg` 单函数、`size() vs count()`、`describe()`
- `get_group()`、遍历分组、`groups` 属性
- 分组后取前 N 条：`groupby().head(n)`

**练习**
1. Occupation：按性别统计平均年龄、按职业+性别交叉统计人数。
2. Apple 股价：按年份分组统计年均收盘价、年最大成交量。
3. 造销售数据：按地区统计销售额、按地区+月份双维度统计。
4. 打印每个分组的前 2 行，观察结果结构。

## D17 · 10/28 周三｜agg / transform / 透视表

**学习内容**
- 命名聚合：`df.groupby('g').agg(均值=('v','mean'), 最大=('v','max'), 笔数=('v','count'))`
- 不同列不同聚合：`agg({'a':'mean','b':'sum'})`
- **transform**：返回与原表等长的结果（组内标准化/中性化的核心工具）
- `filter`：按组级条件整组保留/删除
- `pivot_table(values, index, columns, aggfunc, fill_value, margins)`；`pivot`
- 长宽转换：`melt(id_vars)`、`stack/unstack`

**练习**
1. 用 transform 计算每个行业内个股收益率的**组内 z-score**（这就是因子行业中性化的雏形）。
2. 用 filter 保留"组内样本数 ≥ 3"的行业。
3. 做一张"行业 × 年份"的平均收益率透视表，带行列合计（margins）。
4. 把宽表（各月一列）melt 成长表，再 pivot 还原。

## D18 · 10/29 周四｜窗口函数（量化核心日，本周含金量最高）

**今日目标**：能独立从日线数据算出常用技术指标。

**学习内容**
- `shift(n)`：取 n 期前的值（注意正负方向）；`diff(n)`；`pct_change(n)`（收益率）
- `rolling(window, min_periods).mean()/std()/max()/min()/sum()/apply()`
- `expanding()`：从起点累计
- `ewm(span=).mean()/std()`：指数加权
- `rank(pct=True, method=)`：截面排名；`cumsum/cummax/cummin/cumprod`
- 滚动窗口避免未来函数：t 日信号只能用 t 日及以前数据（思想重点）

**练习（在 Apple 日线数据上完成，做成 `day18_indicators.ipynb`）**
1. 日收益率：`close.pct_change()`；对数收益率：`np.log(close/close.shift(1))`
2. MA5、MA20 均线；20 日滚动波动率（日收益率 std × √252 年化）
3. 20 日动量（`close / close.shift(20) - 1`）；20 日最高/最低
4. RSI 指标（14 日）；EMA20（ewm）
5. 净值曲线：`(1+ret).cumprod()`，画图与收盘价对比

## D19 · 10/30 周五｜matplotlib 绘图

**今日目标**：掌握对象式绘图，能画带净值、回撤、基准对比的研究图。

**学习内容**
- 优先教对象式：`fig, ax = plt.subplots(figsize=(10,5))` → `ax.plot(...)`
- 图类型：`plot / bar / barh / hist / scatter / boxplot`
- 元素：`set_title/xlabel/ylabel/legend/grid/xlim/xticks/annotate`
- 多子图：`plt.subplots(2,1, sharex=True)`；双轴 `twinx()`；参考线 `axhline/axvline`
- **中文配置**：`plt.rcParams['font.sans-serif']=['SimHei']; plt.rcParams['axes.unicode_minus']=False`
- 输出：`figsize/dpi`、`savefig('x.png', dpi=150, bbox_inches='tight')`

**练习**
1. 画 2×2 子图：收盘价+均线、日收益率、收益率分布直方图、成交量柱状。
2. 画净值曲线，并叠加一条基准（可假设无风险利率 3% 年化的直线）。
3. 计算并画出回撤序列（`净值 / cummax - 1`），用 fill_between 填充。
4. 保存 PNG 到 `outputs/` 目录（自己新建）。

## D20 · 10/31 周六｜数据清洗专项 + pandas 题库（4–6 h）

- [ ] 上午：Kaggle Learn 的 **Data Cleaning** 微课程（6 节，含 handling missing values、scaling、parsing dates、character encodings、inconsistent data entry）
- [ ] 下午：牛客网题库「Python 数据分析」专项，完成约 30 题；错题截图记录
- [ ] 编码问题专题：`read_csv(encoding='gbk'/'utf-8')`、`utf-8-sig`（国内 CSV 高频坑）

## D21 · 11/01 周日｜综合小报告 + 复盘

- [ ] 把 D18 指标 + D19 图表合并成 `stock_mini_report.ipynb`：数据读取 → 清洗 → 指标 → 图表 → Markdown 结论（这是多因子项目的最小原型）
- [ ] 整理 `pandas_cheatsheet_2.md`：merge/groupby/transform/pivot/rolling/绘图
- [ ] 教材第 8、9、10 章扫漏；第 11 章选读 resample/shift 部分
- [ ] Git 提交

---

# 第 4 周 · SQL（11/02 – 11/08）

> 平台：牛客「SQL 篇」（MySQL 环境）为主，SQLZOO 学语法，LeetCode 收尾。
> 产出：`week4_sql/` 下按天保存 SQL 文件（`.sql`）+ `sql_cheatsheet.md`。
> 本地可选：Python 自带 `sqlite3` 建库练习（窗口函数以牛客在线环境为准）。

## D22 · 11/02 周一｜环境与基础查询

**学习内容**
- 牛客 SQL 篇界面、运行、看题解；本地 `import sqlite3` 建库建表（了解）
- `SELECT 列 / * / AS 别名 / DISTINCT`
- `WHERE`：比较运算、`BETWEEN AND / IN / LIKE(% _) / IS NULL / AND OR NOT`
- `ORDER BY ... ASC/DESC`（多字段）、`LIMIT n OFFSET m`

**练习**
- SQLZOO：1 SELECT basics、2 SELECT from WORLD、3 SELECT from Nobel
- 牛客：「SQL 必知必会」基础查询章节全部（约 10 题）

## D23 · 11/03 周二｜聚合分组

**学习内容**
- `COUNT(*) / COUNT(列) / SUM / AVG / MAX / MIN`（COUNT 列忽略 NULL）
- `GROUP BY` 单/多列；`HAVING` 分组后过滤（**WHERE 在分组前，HAVING 在分组后**）
- 分组 + 排序组合；去重统计 `COUNT(DISTINCT col)`

**练习**
- SQLZOO：4 SELECT within SELECT（子查询预习）、5 SUM and COUNT
- 牛客：聚合函数 + 分组查询章节全部

## D24 · 11/04 周三｜多表连接

**学习内容**
- `INNER JOIN / LEFT JOIN / RIGHT JOIN / FULL JOIN ... ON`
- 多键连接、连接后加 WHERE、表别名
- **自连接**（同一张表连自己：找相邻日期、上下级、环比的基础）
- `UNION ALL / UNION`（纵向合并，与 JOIN 区分）

**练习**
- SQLZOO：6 The JOIN operation、7 More JOIN
- 牛客：多表查询章节全部
- 自写一题：股价表自连接，求每只股票当日与前一日收盘价（不使用窗口函数）

## D25 · 11/05 周四｜子查询与条件逻辑

**学习内容**
- 子查询位置：`WHERE col IN (子查询)`、`FROM (子查询) AS t`、SELECT 标量子查询
- `EXISTS / NOT EXISTS`；相关子查询（子查询引用外层表）
- `CASE WHEN cond1 THEN v1 WHEN cond2 THEN v2 ELSE v3 END`
- NULL 三值逻辑；`COALESCE(a,b,c)`、`IFNULL`、`NULLIF`

**练习**
- SQLZOO：8 Using Null、8+ Numeric Examples、9 Self join
- 牛客：子查询、条件判断章节全部
- 用 CASE WHEN 把收益率分为涨/跌/平三档并统计天数

## D26 · 11/06 周五｜窗口函数（量化笔试高频，本周重点）

**学习内容**
- 语法：`函数() OVER (PARTITION BY 列 ORDER BY 列 ROWS BETWEEN ... )`
- 排名：`ROW_NUMBER() / RANK() / DENSE_RANK()`（分组取 TopN）
- 偏移：`LAG(列,n) / LEAD(列,n) / FIRST_VALUE / LAST_VALUE`（环比、前后值）
- 聚合窗口：`SUM/AVG/COUNT OVER`（累计求和、移动平均）、`ROWS BETWEEN 2 PRECEDING AND CURRENT ROW`
- 分箱：`NTILE(10)`（十分位分组，分层回测必备）、`CUME_DIST / PERCENT_RANK`

**练习**
- 牛客：窗口函数章节全部（至少 12 题）
- 自写三题：①每个行业市值排名前 3 的股票；②股票相邻交易日价格差（LAG）；③每只股票近 5 日均价（ROWS BETWEEN）
- 学不透就顺延，宁可 D27 少刷 10 题也要把窗口函数写熟

## D27 · 11/07 周六｜牛客集中刷题（4–6 h）

- [ ] 牛客「SQL 必知必会 · 非技术快速入门」全部刷完
- [ ] 「SQL 进阶查询」刷一半以上
- [ ] 累计题量 ≥ 40，整体正确率目标 ≥ 80%
- [ ] 错题全部收藏，写清错误原因（JOIN 丢行？NULL？分组粒度？）

## D28 · 11/08 周日｜LeetCode 数据库 + SQL 复盘

- [ ] LeetCode 数据库：175、181、182、183、196、197、184（7 题，含自连接与窗口）
- [ ] 整理 `sql_cheatsheet.md`：查询顺序（FROM→WHERE→GROUP→HAVING→SELECT→ORDER→LIMIT）、JOIN 对照表、窗口函数模板
- [ ] 衔接练习：用 `pd.read_sql(sql, conn)` 在 Python 里对 sqlite3 跑查询并转 DataFrame，再用 pandas 画一张图
- [ ] Git 提交

---

# 第 5 周 · Linux + Git + 综合实战（11/09 – 11/15）

> 产出：WSL2 可用环境 + GitHub 公开仓库 `quant-learning`（简历可写）。
> Linux 教程：《Linux 工具快速教程》（GitHub `me115/linuxtools_rst`）前 4 章；Git：廖雪峰教程。

## D29 · 11/09 周一｜WSL2 安装与文件操作

**今日目标**：在 Windows 里拥有真实 Linux 环境并能访问 D 盘代码。

**学习内容**
- 安装：管理员 PowerShell 执行 `wsl --install`，重启后装 Ubuntu，设置用户名密码
- 包管理：`sudo apt update && sudo apt upgrade`（慢可换国内镜像源，搜"ubuntu apt 清华源"）
- 路径：`pwd / ls(-l -a -lh) / cd（~ .. -）/ tree`；绝对路径 vs 相对路径
- 文件目录：`mkdir(-p) / rmdir / touch / cp(-r) / mv / rm(-r) / ln -s`
- 查看：`cat / less（q 退出，/ 搜索）/ head -n / tail -n / nl`；编辑器 `nano`
- **关键**：Windows 盘挂载在 `/mnt/c`、`/mnt/d`，你的代码路径是 `/mnt/d/quant-learning`

**练习**
1. 在 WSL 中 `cd /mnt/d/quant-learning && ls -lh` 看到自己的 notebook。
2. 新建 `linux_practice/`，完成创建/复制/重命名/删除一整套操作。
3. 用 less 打开一个 notebook 的 `.ipynb`（本质是 JSON 文本）观察。

## D30 · 11/10 周二｜文本处理、管道、权限与进程

**学习内容**
- `grep -rn "关键词" 路径`（递归+行号）、参数 `-i -v -E`
- `find 路径 -name "*.ipynb" -type f`
- 管道与重定向：`|`、`>`（覆盖）、`>>`（追加）、`2>`、`tee`
- 文本工具：`wc -l`、`sort`、`uniq -c`、`head/tail -f`、`cut -d, -f2`、`awk '{print $1}'`
- 权限：`chmod 755`、`chmod +x`、`sudo`；压缩：`tar -czf a.tar.gz 目录`、`tar -xzf`
- 进程：`ps aux`、`top`（q 退出）、`kill -9 PID`、`df -h`、`du -sh *`

**练习**
1. 在 `quant-learning` 中统计所有 `.ipynb` 文件数量（find + wc）。
2. grep 找出所有用到 `groupby` 的 notebook 文件并列出行号。
3. 把 `ls -l` 的结果重定向到 `files.txt`，再用 sort/wc 处理。
4. 打包整个 week1 目录为 tar.gz 再解压验证。

## D31 · 11/11 周三｜远程登录、Python 环境与后台任务

**学习内容**
- `ssh user@主机 -p 端口`、首次连接确认、`exit`；免密：`ssh-keygen` + `ssh-copy-id`
- 传文件：`scp -r 本地 user@主机:路径`、`rsync -avz`（了解）
- 环境变量：`which python`、`export PATH=...`、写入 `~/.bashrc`、`source ~/.bashrc`、`alias`
- **虚拟环境**：`python3 -m venv .venv` → `source .venv/bin/activate` → `pip install` → `deactivate`；`pip freeze > requirements.txt`
- 后台跑长任务：`nohup python script.py > run.log 2>&1 &`、`jobs/fg`；`tmux new -s work / Ctrl+b d 分离 / tmux attach -t work / tmux ls`

**练习**
1. 在 WSL 的 `linux_practice/` 建 venv，安装 numpy，`pip freeze` 导出 requirements。
2. 写一个 `mc.py`（把 D6 蒙特卡洛改成 .py 脚本，打印结果并写日志）。
3. 用 nohup 后台运行并 `tail -f run.log` 查看；再用 tmux 跑一遍。

## D32 · 11/12 周四｜Git 本地版本管理

**今日目标**：理解工作区/暂存区/版本库三区模型，熟练本地提交。

**学习内容**（廖雪峰教程 1–4 章）
- 配置：`git config --global user.name "..."`、`user.email`
- `git init`；三区：工作区 → `git add` 暂存区 → `git commit -m "msg"` 版本库
- `git status`、`git diff`、`git log --oneline --graph`、`git show`
- `.gitignore`（用 GitHub 官方 Python 模板：忽略 `.ipynb_checkpoints/、.venv/、__pycache__/、data/*.csv`）
- `git checkout -- 文件` 撤销修改、`git reset HEAD 文件` 撤出暂存（谨慎用 `--hard`）

**练习**
1. 在 `quant-learning` 执行 `git init`，配置好用户名邮箱。
2. 写好 `.gitignore`，把前五周 notebook 分批 add/commit（按周为单位，至少 5 个 commit）。
3. 故意修改一个文件，用 status/diff 观察变化，再撤销。

## D33 · 11/13 周五｜GitHub 远程仓库

**学习内容**
- 生成 SSH key：`ssh-keygen -t ed25519 -C "邮箱"`，复制 `~/.ssh/id_ed25519.pub` 公钥添加到 GitHub → Settings → SSH keys
- 验证：`ssh -T git@github.com`
- GitHub 网页 New repository（命名 `quant-learning`，**不勾** README/license，避免首次冲突）
- `git remote add origin git@github.com:用户名/quant-learning.git`
- `git branch -M main`、`git push -u origin main`
- `git clone`、`git pull`、`git fetch`

**练习**
1. 把本地仓库推送到 GitHub，网页上确认目录、notebook、提交历史都在。
2. 在 GitHub 网页编辑 README，回本地 `git pull` 拉取。
3. 在 WSL 中把仓库 clone 到另一个目录验证。

## D34 · 11/14 周六｜分支、合并与冲突

**学习内容**（廖雪峰分支管理章节）
- `git branch dev`、`git switch -c dev`（或 checkout -b）、`git switch main`
- `git merge dev`：快进合并与三方合并
- **冲突**：两个分支改同一文件同一行 → 冲突标记 `<<<<<<< ======= >>>>>>>` → 手动编辑 → add → commit
- `git stash`（临时保存半成品）、`git revert`（安全撤销某次提交）
- 协作流程了解：fork → 建分支 → commit → Pull Request

**练习**
1. 建 dev 分支，在 README 加一段内容并提交，切回 main 合并。
2. 故意在 main 和 dev 上修改 README 同一行，制造并解决一次冲突。
3. 用 stash 在两个任务间切换半成品。

## D35 · 11/15 周日｜综合实战 + 五周总复盘（4–6 h）

**仓库整理（目标：陌生人打开能看懂）**

```
quant-learning/
├── README.md              # 项目简介、环境版本、目录说明、成果展示
├── requirements.txt       # pip freeze
├── .gitignore
├── week1_numpy/           # 含 day06_monte_carlo.ipynb
├── week2_pandas/
├── week3_pandas_advanced/ # 含 stock_mini_report.ipynb
├── week4_sql/
├── week5_linux_git/
├── data/                  # 数据（大文件不入库，写获取方式）
└── outputs/               # 图表
```

- [ ] README 必写：本机环境版本、每周学了什么、蒙特卡洛实验结论（加速比/误差）、mini report 截图或图表
- [ ] 全程命令行 add/commit/push；在 WSL 中 clone 到全新目录从头运行所有 notebook 验证
- [ ] 对照下方验收清单逐项自测，不达标项记录，下周补

---

## 第五周末验收标准（对标实习第一周工作）

### NumPy
- [ ] 不看笔记手写：造 10000×252 随机矩阵 → 按列标准化 → 广播运算 → 聚合统计
- [ ] 能口述广播三规则；能判断任意两个形状能否广播
- [ ] 独立完成蒙特卡洛定价，向量化版与 for 版耗时差异有量化记录

### pandas
- [ ] 给一份脏 CSV（缺失/重复/类型错误/日期混乱），30 分钟内完成清洗
- [ ] 不查文档写出：read_csv 常用参数、loc/iloc、groupby+agg、merge 四种连接、rolling 指标
- [ ] 能从日线数据独立算出收益率、均线、波动率、动量并画净值/回撤图

### SQL
- [ ] 牛客 SQL 篇累计 ≥ 40 题，正确率 ≥ 80%
- [ ] 窗口函数（ROW_NUMBER/LAG/累计求和/NTILE）能独立默写
- [ ] 能说清 WHERE 与 HAVING、JOIN 四种方式、UNION 与 JOIN 的区别

### Linux
- [ ] 能 ssh 登录服务器、scp 传文件
- [ ] 能用 find/grep/管道定位文件与内容，看懂 chmod 权限
- [ ] 会建 venv、会用 nohup/tmux 跑后台任务并查日志

### Git / GitHub
- [ ] 本地 init/add/commit/log、远程 push/pull/clone、分支 merge 与冲突解决全程独立完成
- [ ] GitHub 上有结构清晰、带 README 的公开仓库 `quant-learning`

---

## 常见坑位预案

| 现象 | 原因 / 处理 |
|---|---|
| pip 下载超时 | 命令加 `-i https://pypi.tuna.tsinghua.edu.cn/simple` |
| notebook 选不到内核 | Ctrl+Shift+P → Python: Select Interpreter → 选 3.12.5 |
| `import` 报 ModuleNotFoundError | 包装到了别的 Python：notebook 里跑 `import sys; print(sys.executable)` 核对 |
| 改了切片原数组也变了 | 切片是视图，需要独立数据时加 `.copy()` |
| 多条件筛选报错 | 必须用 `& \| ~` 且每个条件用括号括起来 |
| read_csv 中文乱码 | 试 `encoding='gbk'`，再试 `'utf-8-sig'` |
| resample 报 Invalid frequency | pandas 3.0 用 `'ME'/'YE'/'QE'/'h'/'min'` |
| applymap 报不存在 | pandas 3.0 改用 `DataFrame.map()` |
| WSL 找不到 D 盘 | 路径是 `/mnt/d/...`，不是 Windows 的 `D:\` |
| git push 提示认证失败 | 确认用的是 SSH 地址且公钥已添加；`ssh -T git@github.com` 验证 |
| 任何红色报错 | 先读最后一行 → 复制关键句搜索 → 解决不了带着完整报错提问 |

---

## 完成之后（11/16 起）的衔接

1. **LeetCode**：按总计划继续热题 100 收尾（堆 215/347、拓扑 207、LRU 146），每周保持 3–5 题。
2. **概率题**：启动绿皮书《A Practical Guide to Quantitative Finance Interviews》。
3. **量化项目一（多因子）**：数据栈已齐，按"数据获取 → 因子计算 → IC/IR → 分层回测 → 绩效图"推进；届时可让我提供分步框架。
