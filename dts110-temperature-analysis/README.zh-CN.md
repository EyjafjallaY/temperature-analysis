# 历史温度趋势分析与回归模型评估

[English](README.md)

使用 Python 分析 21 个城市在 1961—2015 年间的 421,848 条日温度记录，比较年度聚合、五年移动平均和不同阶数的回归模型，并在后续年份上评估预测误差。

本项目的数据集与两项复用的辅助实现来自 [MIT OCW 温度分析资源](https://ocw.mit.edu/courses/6-0002-introduction-to-computational-thinking-and-data-science-fall-2016/resources/ps5/)。来源、贡献划分与许可见[来源说明](docs/provenance.md)和 [LICENSE](LICENSE)。

## 主要结果

训练区间为 1961—2009 年，测试区间为 2010—2015 年。两个区间分别计算移动平均，窗口最多包含五年。

| 模型阶数 | 训练 R² | 测试 RMSE（°C） |
| --- | ---: | ---: |
| 1 | 0.9250 | 0.0884 |
| 2 | 0.9448 | 0.2118 |
| 20 | 0.9724 | 1.4912 |

目标是这组城市的平滑年度均温。线性模型在六个测试年份的对比中误差最低；20 阶模型训练拟合度较高，但产生数值稳定性警告，测试误差也较大。

![线性模型在测试年份上的表现](figures/linear_testing.png)

## 阅读顺序

1. [Notebook](temperature_analysis.ipynb)：代码、实验流程和已有断言测试。
2. [分析说明](docs/analysis.md)：各项实验、结果、解释边界与应用构想。
3. [数据说明](docs/data.md)：字段、范围、来源、校验值和已知数据问题。
4. [来源说明](docs/provenance.md)：外部资源、项目实现部分与使用许可。

`figures/` 保留十张原始结果图。五年移动平均的线性拟合图也对应 1 阶模型训练结果，因而只保留一张。

## 运行

使用 Python 3.11。创建项目环境并激活后安装依赖：

```text
python -m venv .venv
```

Windows 激活命令为 `.venv\Scripts\activate`；macOS/Linux 使用 `source .venv/bin/activate`。

```text
python -m pip install -r requirements.txt
```

在支持 Notebook 的 IDE 中打开 `temperature_analysis.ipynb`，选用该环境，重启内核并依次运行所有单元。`data.csv` 与 Notebook 保持在项目根目录，执行时的工作目录也应为项目根目录。

有可用 `python3` 内核时，可以无界面执行并另存结果：

```text
jupyter execute temperature_analysis.ipynb --kernel_name=python3 --timeout=120 --output=executed
```

## 复现核验

2026-10-08 已在现有 Python 3.11.14 环境的新内核中从头执行：22 个原始代码单元全部完成，6 组已有断言测试通过，主要结果在四位小数上与保存的报告结果一致。20 阶模型的数值稳定性警告保留。

保存的 Notebook 输出与 PNG 展示上述实验结果。本次在现有环境中完成整本 Notebook 的运行核验；未验证重新安装依赖后的运行。

## 解释与使用范围

城市平均采用等权重，不能直接代表全球或按面积加权的全国温度。平滑后的 R² 不等于预测准确率；年内标准差也不能直接代表极端天气频次。具体口径见分析说明。

公开材料沿用上游的 **CC BY-NC-SA 4.0** 要求：署名、非商业使用、以相同许可分享。它允许按条件公开分享，但不等同于允许任意商业使用的软件开源许可。项目不代表任何机构的认可或背书。
