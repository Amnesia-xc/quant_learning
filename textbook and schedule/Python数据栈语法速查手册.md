# Python 数据栈语法速查手册

> 五周学习内容速查（NumPy / pandas / SQL / Linux / Git），用于快速回忆记不清的语法。
> 环境基准：Python 3.12.5、NumPy 2.5.x、pandas 3.0.6、SQLite 3.49、Git 2.56。
> 标 `⚠️` 的为版本兼容/易错点。

---

# 一、NumPy

## 1. 创建数组

```python
import numpy as np

np.array([1, 2, 3])              # 从列表创建
np.zeros((3, 4))                 # 全 0
np.ones((2, 5))                  # 全 1
np.full((3, 3), 7)               # 填充指定值
np.empty((2, 2))                 # 不初始化（值随机，速度快）
np.arange(0, 10, 2)              # 等差 [0,2,4,6,8]
np.linspace(0, 1, 5)             # 5 个等距点
np.eye(3)                        # 单位矩阵
np.random.rand(3, 4)             # 0~1 均匀随机
```

## 2. 查看属性

```python
a.ndim        # 维度数
a.shape       # 形状（元组）
a.size        # 元素总数
a.dtype       # 数据类型
a.reshape(3, 4)          # 改形状（元素数须一致）
a.ravel()                # 展平为一维
a.T                      # 转置
```

## 3. 数据类型

```python
a.astype(np.float64)      # 类型转换
# 常用：int32/int64、float32/float64、bool、str
```

## 4. 索引与切片

```python
a[0]                # 第一个
a[-1]               # 最后一个
a[1:4]              # 切片（左闭右开）
a[:2, 1:3]          # 多维切片
a[a > 5]            # 布尔索引
a[[0, 2, 4]]        # 花式索引
a[0, 1] = 9         # 赋值
```

⚠️ 切片是**视图**，改它会影响原数组；需要独立副本用 `a[...].copy()`。

## 5. 轴 axis

```python
a.sum(axis=0)       # 沿轴 0（跨行，按列聚合）
a.sum(axis=1)       # 沿轴 1（跨列，按行聚合）
a.mean(axis=0)
# 记忆：axis=k 表示沿第 k 个方向"压缩"
```

## 6. 广播规则

```python
# 两数组运算时，形状从右往左逐维比较：
# 1) 维度相等，或其中一个为 1，则兼容；
# 2) 维度缺失的一侧在左侧补 1；
# 3) 为 1 的维度自动复制扩展。
a + np.array([1, 2, 3])      # 每行加向量
(3,4) + (4,)   -> (3,4) ✅
(3,4) + (3,)   -> 报错 ❌（4≠3）
```

## 7. 通用函数 ufunc（逐元素）

```python
np.sqrt(a)、np.exp(a)、np.log(a)
np.abs(a)、np.maximum(a, b)
np.add / multiply / power
np.where(cond, x, y)         # 条件选择
```

## 8. 聚合统计

```python
a.sum()、a.mean()、a.std()、a.var()
a.min()、a.max()
a.argmin()、a.argmax()       # 最小/最大值索引
np.median(a)、np.percentile(a, 95)
np.cumsum(a)、np.cumprod(a)  # 累计和/累计积
```

⚠️ `np.std` 默认 `ddof=0`（总体标准差）；pandas 默认 `ddof=1`（样本）。

## 9. 线性代数

```python
A @ B                  # 矩阵乘法（也可用 np.dot）
np.linalg.inv(A)       # 逆矩阵
np.linalg.det(A)       # 行列式
np.linalg.eig(A)       # 特征值/特征向量
np.linalg.solve(A, b)  # 解 Ax=b（优先于 inv）
```

## 10. 随机数（新版推荐 Generator）

```python
rng = np.random.default_rng(seed=42)
rng.random((3, 3))             # 均匀
rng.normal(0, 1, (100,))       # 正态
rng.integers(0, 10, 5)         # 随机整数
rng.choice([1, 2, 3], size=10) # 抽样
rng.shuffle(a)                 # 原地打乱
```

## 11. 向量化/蒙特卡洛

```python
# 核心思想：用整体数组运算替代 Python for 循环
paths = rng.normal(0, 1, (n_sims, n_steps))
prices = np.cumprod(1 + paths, axis=1)   # 一次性模拟所有路径
```

---

# 二、pandas

## 1. 读写文件

```python
import pandas as pd

df = pd.read_csv('a.csv')
df = pd.read_csv('a.tsv', sep='\t')
pd.read_excel('a.xlsx', sheet_name=0)
df.to_csv('out.csv', index=False)
df.to_excel('out.xlsx', index=False)
# 常用参数：header、names、usecols、dtype、parse_dates、na_values、encoding
```

## 2. Series / DataFrame

```python
pd.Series([1, 2, 3], index=['a', 'b', 'c'])
pd.DataFrame({'x': [1, 2], 'y': [3, 4]})
df.head()、df.tail()、df.sample(5)
df.shape、df.columns、df.index、df.dtypes、df.info()
df.describe()           # 数值列统计
df['new'] = df['x'] * 2 # 新建列
```

## 3. 选择数据

```python
df['col']               # 选列（Series）
df[['a', 'b']]          # 选多列（DataFrame）
df.loc[行标签, 列标签]   # 按标签
df.iloc[行位置, 列位置]  # 按整数位置
df.loc[df['x'] > 0]     # 条件筛选
df[(df['a'] > 1) & (df['b'] < 5)]   # 多条件
```

⚠️ 多条件用 `& | ~`，**每个条件必须加括号**；不能用 `and/or`。

## 4. 数据清洗

```python
df.isna()、df.isnull()、df.notna()
df.dropna()                 # 删缺失（axis、how、subset、thresh）
df.fillna(0)                # 填充（也可用 df['c'].mean()）
df.duplicated()、df.drop_duplicates()
df['c'] = df['c'].astype(int)
df.rename(columns={'old': 'new'})
df.replace(old, new)
```

## 5. 字符串方法（.str）

```python
df['name'].str.lower()、str.upper()
str.contains('x')、str.startswith('a')
str.strip()、str.replace('a', 'b', regex=False)
str.split(',', expand=True)、str.len()
```

⚠️ pandas 3.0 中 `str.replace` 须显式 `regex=False`（否则按正则处理）。

## 6. apply / map

```python
df['c'].map({1: 'A', 2: 'B'})     # 映射
df['c'].apply(lambda x: x * 2)    # 函数
df.apply(np.sum, axis=0)
```

⚠️ pandas 3.0 已移除 `applymap`，逐元素用 `DataFrame.map()`。

## 7. 合并 concat / merge

```python
pd.concat([df1, df2], axis=0)          # 堆叠（axis=1 横向）
pd.merge(left, right, on='id', how='inner')
# how：inner / left / right / outer
# 键名不同：left_on、right_on
df1.join(df2)                          # 按索引连接
```

## 8. groupby 分组

```python
df.groupby('cat')['val'].sum()
df.groupby('cat').agg(总=('v','sum'), 均=('v','mean'), 数=('v','count'))
df.groupby('cat')['v'].transform('mean')  # 广播回原行数
# 常用聚合：sum/mean/count/min/max/median/std/nunique
```

## 9. 透视表

```python
df.pivot_table(index='cat', columns='yr',
               values='v', aggfunc='mean',
               fill_value=0, margins=True)
```

## 10. 窗口函数（量化核心）

```python
s.rolling(window=5).mean()      # 滚动均值
s.rolling(20).std()             # 滚动波动率
s.rolling(60).max()、min()
s.shift(1)                      # 前值
s.pct_change()                  # 简单收益率
s.cummax()                      # 历史最高（算回撤用）
s.expanding().mean()            # 扩展窗口
```

## 11. 时间序列

```python
pd.to_datetime(df['date'])
df.set_index('date').sort_index()
df.resample('ME').last()        # 月末
df['date'].dt.year、dt.month、dt.dayofweek
```

⚠️ pandas 3.0 频率别名：`ME`(月末)、`YE`(年末)、`QE`(季末)、`h`、`min`；旧的 M/Y 已弃用。

## 12. 收益/净值/回撤

```python
ret = s.pct_change()
nav = (1 + ret).cumprod()                 # 净值
drawdown = nav / nav.cummax() - 1         # 回撤序列
mdd = drawdown.min()                      # 最大回撤
```

⚠️ 若用对数收益 `log_ret = np.log(s / s.shift(1))`，净值用 `np.exp(log_ret.cumsum())`，不能直接对对数收益 `+1` 累乘。

## 13. 绘图

```python
import matplotlib.pyplot as plt

df.plot()、df['c'].plot(kind='line')
# kind：line/bar/hist/box/scatter/area
nav.plot(title='NAV'); plt.show()
```

## 14. 模糊匹配

```python
from thefuzz import fuzz, process
fuzz.ratio('abc', 'abd')
process.extractOne('北京', candidates, score_cutoff=80)
```

## 15. 版本兼容补充

- ⚠️ 已移除 `df.append`，用 `pd.concat`。
- ⚠️ 整数索引取末值用 `.iloc[-1]`。
- pandas 默认 `ddof=1`。

---

# 三、SQL（SQLite）

## 1. 基础查询

```sql
SELECT col1, col2 FROM t;
SELECT * FROM t WHERE x > 10;
ORDER BY x DESC, y ASC;
LIMIT 10;
DISTINCT col;
```

## 2. 条件/操作符

```sql
WHERE a = 1 AND b = 2 OR c = 3
WHERE x IN (1, 2, 3)
WHERE x BETWEEN 1 AND 10
WHERE name LIKE '张%'      -- % 任意多个，_ 单个
IS NULL / IS NOT NULL
```

## 3. 聚合与分组

```sql
SELECT cat, COUNT(*), SUM(v), AVG(v), MAX(v), MIN(v)
FROM t
GROUP BY cat
HAVING COUNT(*) > 5;
```

- `COUNT(*)` 计所有行；`COUNT(col)` 不计 NULL。
- WHERE 在分组前过滤行；HAVING 在分组后过滤组。

## 4. 多表连接

```sql
SELECT * FROM a JOIN b ON a.id = b.id;        -- 内连接
LEFT JOIN        -- 左表全保留，右表无匹配补 NULL
RIGHT JOIN       -- SQLite 3.39+ 支持
FULL OUTER JOIN  -- ⚠️ SQLite 不支持
-- 自连接：给同一张表起两个别名
```

## 5. 子查询

```sql
-- WHERE 中
SELECT * FROM t WHERE id IN (SELECT id FROM t2);
-- FROM 中（派生表）
SELECT x FROM (SELECT ... ) AS sub;
-- SELECT 中
SELECT *, (SELECT ...) AS col FROM t;
EXISTS (SELECT 1 FROM t2 WHERE ...)
```

⚠️ `NOT IN` 遇到子查询含 NULL 会整体返回空，改用 `NOT EXISTS`。

## 6. CASE 条件

```sql
CASE WHEN score >= 90 THEN '优'
     WHEN score >= 60 THEN '及格'
     ELSE '不及格' END
```

## 7. 窗口函数

```sql
ROW_NUMBER() OVER (PARTITION BY cat ORDER BY score DESC)
RANK()        -- 并列后跳号
DENSE_RANK()  -- 并列不跳号
LAG(col, 1) OVER (ORDER BY d)
LEAD(col, 1) OVER (ORDER BY d)
SUM(v) OVER (PARTITION BY cat ORDER BY d
             ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
NTILE(4) OVER (ORDER BY v)
```

## 8. 逻辑执行顺序

```
FROM/JOIN → WHERE → GROUP BY → 聚合 → HAVING → 窗口 → SELECT → ORDER BY → LIMIT
```

⚠️ 窗口函数不能直接塞进 GROUP BY 聚合参数；先在子查询算窗口结果，外层再聚合。

## 9. pandas ↔ SQL 衔接

```python
import sqlite3
conn = sqlite3.connect('x.db')
df = pd.read_sql("SELECT * FROM t", conn)
df.to_sql('t', conn, if_exists='replace', index=False)
```

---

# 四、Linux（Bash）

## 1. 文件与目录

```bash
pwd                 # 当前路径
ls -lh              # 列表（-a 含隐藏，-h 易读）
cd dir、cd ..、cd ~、cd -
mkdir -p a/b        # 递归建目录
touch f.txt
cp -r src dst、mv src dst
rm -rf dir          # 危险，慎用
cat、head、tail -n 20、less（q 退出）
find . -name "*.py" -type f
```

## 2. 文本处理

```bash
grep "word" f              # 搜内容
grep -rn "x" dir -i        # 递归/行号/忽略大小写
grep -v "x"                # 反向过滤
wc -l、wc -w
sort、uniq -c              # 排序/去重计数
cut -d',' -f1
awk '{print $1}'
```

## 3. 管道与重定向

```bash
cmd1 | cmd2                # 前一个输出给后一个
> file                     # 覆盖写入
>> file                    # 追加
2> err.log                 # 错误重定向
2>&1                       # 错误合并到标准输出
```

## 4. 权限

```bash
chmod +x script.sh
chmod 755 f        # r=4 w=2 x=1；755=rwxr-xr-x
sudo cmd
./script.sh        # 运行当前目录可执行文件
```

## 5. 进程

```bash
ps aux
ps aux | grep python
top（q 退出）
kill PID、kill -9 PID       # 纯数字 PID 不加 $
jobs
bg、fg
pkill name
df -h、du -sh *
```

⚠️ `$` 只加在变量名前（`$!`、`$PATH`）；纯数字 PID 直接写，不加 `$`。

## 6. 环境变量

```bash
which python
echo $PATH                 # 冒号分隔的目录
export MY_VAR=value
alias ll='ls -lh'、unalias ll
# 持久化：写入 ~/.bashrc，再 source ~/.bashrc
```

## 7. 虚拟环境

```bash
python3 -m venv .venv
source .venv/bin/activate   # 激活（提示符出现 (.venv)）
deactivate                 # 退出
pip install -r requirements.txt
pip freeze > requirements.txt
```

## 8. 后台任务

```bash
nohup python3 s.py > run.log 2>&1 &   # 关终端不退出
tail -f run.log                       # 跟踪日志
tmux new -s work                      # 建会话
# Ctrl+b 然后 d：分离
tmux ls、tmux attach -t work、tmux kill-session -t work
```

## 9. 打包

```bash
tar -czf a.tar.gz dir      # 压缩
tar -tzf a.tar.gz          # 查看
tar -xzf a.tar.gz -C dst   # 解压
```

## 10. 远程

```bash
ssh user@host -p 22
scp -r local user@host:/path
ssh-keygen、ssh-copy-id user@host
```

## 11. 路径/编码备忘

- Windows 盘在 WSL：`/mnt/c`、`/mnt/d`。
- PowerShell 5.1 裸 `>` 写 UTF-16，写 UTF-8 用 `[IO.File]::WriteAllText(...)`。

---

# 五、Git / GitHub

## 1. 配置

```bash
git config --global user.name "name"
git config --global user.email "a@b.com"
git config --list
```

## 2. 三区模型

```
工作区 --git add--> 暂存区 --git commit--> 版本库
```

## 3. 基础操作

```bash
git init
git status、git status -s
git add file、git add .
git commit -m "message"
git diff                 # 工作区 vs 暂存
git diff --cached        # 暂存 vs 版本库
git log --oneline --graph
git show HEAD
```

状态码：`??` 未跟踪；` M` 工作区改（红）；`M ` 已暂存（绿）；`A` 新增暂存。

## 4. 分支

```bash
git branch               # 列分支
git branch dev           # 建分支
git switch dev           # 切换
git switch -c dev        # 建并切换
git switch main
git merge dev            # 合并
git branch -d dev        # 删分支
```

## 5. 撤销

```bash
git checkout -- file       # 丢弃工作区修改（不可恢复，慎用）
git restore file           # 新版等价写法
git reset HEAD file        # 撤出暂存，改动保留
git revert <commit>        # 新增反向提交（安全，不改写历史）
git stash、git stash pop   # 临时存/恢复半成品
```

撤销合并提交：`git revert -m 1 <merge-commit>`（`-m 1` 保留主线）。

## 6. 远程仓库

```bash
git remote add origin git@github.com:user/repo.git
git remote -v
git branch -M main
git push -u origin main
git push                   # 后续推送
git pull                   # 拉取并合并
git fetch                  # 只下载不合并
git clone url              # 首次完整复制
```

## 7. 冲突解决

```
<<<<<<< HEAD
当前分支内容
=======
被合并分支内容
>>>>>>> branch
```
手动编辑成最终内容 → `git add` → `git commit`。

## 8. 协作流程

fork → 建分支 → commit → push → Pull Request → review → merge。

---

# 附：高频易错点速记

| 易错点 | 正确做法 |
|---|---|
| 切片改了原数组 | 需要独立数据加 `.copy()` |
| 多条件筛选报错 | 用 `& \| ~`，各条件加括号 |
| 标准差口径不一 | NumPy ddof=0，pandas ddof=1 |
| 对数收益算净值 | 用 `exp(cumsum)`，不 +1 累乘 |
| NOT IN 撞 NULL | 改用 NOT EXISTS |
| 窗口函数放进聚合 | 先子查询分层 |
| PowerShell 文件变二进制 | 用 WriteAllText 写 UTF-8 |
| 纯数字 PID 加 $ | 直接写数字，$ 只加变量 |
| revert 合并提交报错 | 加 `-m 1` |
| pandas 旧语法失效 | applymap→map、append→concat、M→ME |

> （注：部分内容由豆包 AI 生成）