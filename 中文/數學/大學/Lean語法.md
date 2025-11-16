# Lean 語法

以下是 LaTeX 與 Lean 中常見的語法與邏輯符號的對照表，涵蓋了基本邏輯符號及相關命令：

| **符號**            | **LaTeX 語法**       | **Lean 語法**        | **描述**            |
| ------------------------- | -------------------------- | -------------------------- | ------------------------- |
| `∧` (AND)              | `\land`                  | `∧`                     | 邏輯 AND (且)             |
| `∨` (OR)               | `\lor`                   | `∨`                     | 邏輯 OR (或)              |
| `¬` (NOT)              | `\neg`                   | `¬`                     | 邏輯 NOT (非)             |
| `→` (Implies)          | `\rightarrow` or `\to` | `→` or `→`           | 邏輯蘊涵                  |
| `↔` (Iff)              | `\leftrightarrow`        | `↔`                     | 若且唯若 (當且僅當)       |
| `∀` (For all)          | `\forall`                | `∀`                     | 全稱量化 (對所有...)      |
| `∃` (There exists)     | `\exists`                | `∃`                     | 存在量化 (存在...)        |
| `⊢` (Proves)           | `\vdash`                 | `⊢`                     | 證明                      |
| `⊨` (Models)           | `\models`                | `⊨`                     | 模型 (符合)               |
| `∈` (Element of)       | `\in`                    | `∈`                     | 元素                      |
| `⊂` (Subset)           | `\subset`                | `⊂`                     | 真子集                    |
| `⊆` (Subset or equal)  | `\subseteq`              | `⊆`                     | 子集或等於                |
| `⊥` (False)            | `\bot`                   | `⊥`                     | 假命題                    |
| `⊤` (True)             | `\top`                   | `⊤`                     | 真命題                    |
| `≠` (Not equal)        | `\neq`                   | `≠`                     | 不等於                    |
| `=` (Equals)            | `=`                      | `=`                      | 等於                      |
| `≤` (Less or equal)    | `\leq`                   | `≤`                     | 小於或等於                |
| `≥` (Greater or equal) | `\geq`                   | `≥`                     | 大於或等於                |
| `∅` (Empty set)        | `\emptyset`              | `∅`                     | 空集                      |
| `∩` (Intersection)     | `\cap`                   | `∩`                     | 交集                      |
| `∪` (Union)            | `\cup`                   | `∪`                     | 聯集                      |
| `∖` (Set difference)   | `\setminus`              | `\`                      | 集合差 (相對補集)         |
| `ℕ` (Natural numbers)  | `\mathbb{N}`             | `ℕ`                     | 自然數                    |
| `ℤ` (Integers)         | `\mathbb{Z}`             | `ℤ`                     | 整數                      |
| `ℚ` (Rational numbers) | `\mathbb{Q}`             | `ℚ`                     | 有理數                    |
| `ℝ` (Real numbers)     | `\mathbb{R}`             | `ℝ`                     | 實數                      |
| `∑` (Summation)        | `\sum`                   | `Σ`                     | 總和                      |
| `∏` (Product)          | `\prod`                  | `Π`                     | 乘積                      |
| `⟨x, y⟩` (Pairing)    | `\langle x, y \rangle`   | `(x, y)` or `⟨x, y⟩` | 配對                      |
| `∥x∥` (Norm)          | `\| x \|`                  | `∥x∥`                  | 範數 (通常用於向量的長度) |

## 備註

1. LaTeX 語法中的大多數符號可以直接應用在數學環境中，通常需要包含在 `$$ ... $$` 內或 `\begin{equation} ... \end{equation}`。
2. Lean 中的大部分符號可以直接用來撰寫數學證明，並且在 Lean 中，邏輯符號通常會配合定理或公式來使用。
