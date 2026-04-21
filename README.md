# 数据结构课程设计（data-structure）

## 项目简介
本仓库包含多个独立的数据结构/算法实验程序，涵盖链表、队列、栈、树、图、并查集、哈夫曼编码与排序算法性能对比等内容。

## 本次整理结果
1. 已删除目录下全部 `exe` 可执行文件。
2. 已将数字命名的 `cpp` 文件重命名为语义化名称。

## C++ 文件重命名对照

| 旧文件名 | 新文件名 | 主题 |
|---|---|---|
| `1.cpp` | `process_linked_lists_monitor.cpp` | 进程信息链表管理 |
| `2.cpp` | `maze_bfs_queue_stack.cpp` | 迷宫 BFS（队列+栈回溯路径） |
| `3.cpp` | `family_tree_child_sibling.cpp` | 家谱树（孩子-兄弟表示法） |
| `5.cpp` | `huffman_coding_tree.cpp` | 哈夫曼编码/解码 |
| `6.cpp` | `metro_min_days_kruskal.cpp` | Kruskal 最小工期问题 |
| `7.cpp` | `subway_path_bfs.cpp` | 地铁路径规划（最少站点/最少换乘） |
| `9.cpp` | `sorting_algorithms_benchmark.cpp` | 多排序算法性能测试 |
| `19.cpp` | `graph_mst_prim_kruskal.cpp` | 图的最小生成树（Prim + Kruskal） |
| `main.cpp` | `source_text_viewer.cpp` | 文本读取演示 |

## 各源码文件的数据结构分析

### 1) `process_linked_lists_monitor.cpp`
- 核心数据结构：
  - 单链表 `SLNode` / `SListInfo`：存储运行中进程，按内存占用插入排序。
  - 双链表 `DLNode` / `DListInfo`：存储结束进程信息，按持续时间插入排序。
- 关键点：
  - 通过遍历 Linux `/proc` 获取进程信息（依赖 `unistd.h`、`/proc/stat`）。
  - 展示链表插入、遍历、销毁等基本操作。

### 2) `maze_bfs_queue_stack.cpp`
- 核心数据结构：
  - 循环队列（数组实现）`queue`：用于 BFS 扩展节点。
  - 顺序栈（动态扩容）`stack`：用于逆序输出路径。
  - `point` 坐标结构体与 `prev` 前驱数组：记录路径。
- 关键点：
  - BFS 保证找到最短步数路径（按边数）。
  - 使用 `2.txt` 作为迷宫输入。

### 3) `family_tree_child_sibling.cpp`
- 核心数据结构：
  - 通用树（孩子-兄弟链表）`TreeNode`：`firstchild + nextbrother`。
  - `unordered_map<string, Tree>`：构建阶段用于姓名到节点的快速索引。
  - `people` 结构体：封装家谱成员属性。
- 关键点：
  - 支持按姓名/生日查询、插入、删除、修改、代际打印、关系判断。
  - 树数据持久化到 `3.txt`。

### 4) `huffman_coding_tree.cpp`
- 核心数据结构：
  - 哈夫曼树节点 `Node`（二叉树）。
  - `unordered_map<char, HTree>`：统计字符频次并保存叶节点。
- 关键点：
  - 构建哈夫曼树后生成字符编码表（`Huffman.txt`）。
  - 对 `source.txt` 编码到 `code.dat`，再解码到 `recode.txt`。

### 5) `metro_min_days_kruskal.cpp`
- 核心数据结构：
  - 边集数组 `edge e[]`。
  - 并查集 `root[]`（路径压缩）。
- 关键点：
  - 先按边权排序，再执行 Kruskal。
  - 输出“连接 1 到 n 所需最短工期”对应的最大边权。

### 6) `subway_path_bfs.cpp`
- 核心数据结构：
  - 路线链表 `route_list`（每条线路一条链）。
  - 站点邻接关系链表 `relation`（站点间连通关系）。
  - `station_map`：以站点 ID 为索引组织邻接信息。
  - STL `queue`/`stack`：用于 BFS 与路径还原。
- 关键点：
  - `BFS_least_visit`：求最少经过站点路径。
  - `BFS_least_change`：求最少换乘线路路径。
  - 输入数据文件为 `7.txt`。

### 7) `sorting_algorithms_benchmark.cpp`
- 核心数据结构：
  - 多组顺序数组 `arr1~arr8`：用于并行测试不同排序算法。
  - 统计矩阵 `arr9[9][11]`：记录不同轮次的耗时。
  - `unordered_map<int,int>` + `pair<int,int>[]`：统计元素频次并排序输出。
- 关键点：
  - 包含冒泡、插入、选择、希尔、快排、堆排、归并、基数排序。
  - 使用 `GetTickCount()`（`windows.h`）计时，偏 Windows 环境。

### 8) `graph_mst_prim_kruskal.cpp`
- 核心数据结构：
  - 邻接矩阵 `vector<vector<int>> arcs`（Prim 使用）。
  - 边集数组 `edge e[]` + 并查集 `root[]`（Kruskal 使用）。
- 关键点：
  - 同一输入下输出 Prim 与 Kruskal 两种最小生成树结果。

### 9) `source_text_viewer.cpp`
- 核心数据结构：
  - 基本字符流读取（`ifstream` + `char`）。
- 关键点：
  - 将 `source.txt` 内容逐字符输出，属于 I/O 基础示例。

## 数据文件说明
- `2.txt`：迷宫地图输入。
- `3.txt`：家谱成员数据。
- `7.txt`：地铁线路站点数据。
- `9.txt`：排序测试随机数据。
- `source.txt`：哈夫曼编码源文本。
- `Huffman.txt`：字符频次与编码表输出。
- `code.dat`：哈夫曼编码结果。
- `recode.txt`：解码结果文本。

## 编译与运行示例
```bash
g++ -std=c++17 maze_bfs_queue_stack.cpp -o maze
./maze
```

```bash
g++ -std=c++17 graph_mst_prim_kruskal.cpp -o mst
./mst
```

说明：
- `process_linked_lists_monitor.cpp` 依赖 Linux `/proc`，建议在 Linux 环境运行。
- `sorting_algorithms_benchmark.cpp` 使用 `windows.h`，建议在 Windows 环境编译运行。
