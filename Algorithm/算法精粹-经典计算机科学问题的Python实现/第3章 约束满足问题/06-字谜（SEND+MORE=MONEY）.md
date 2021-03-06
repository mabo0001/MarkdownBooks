### 3.5　字谜（SEND+MORE=MONEY）

字谜（SEND+MORE=MONEY）是一种数字密码谜题，目标是要找到替换字母的数字使数学式成立。该问题中的每个字母都代表一个数字（0～9）。同一个数字只会用一个字母来表示。如果字母重复出现，则表示最后的解中也有数字重复。

如果要人工求解字谜问题，那么把单词排成竖式会很有用。

```c
  SEND
 +MORE
=MONEY
```

只要运用一点代数知识和直觉，人工求解一定是可行的。但一个相当简单的计算机程序可以通过蛮力（brute-forcing）试探大量可能的结果来更快地求解。下面把SEND + MORE = MONEY谜题表示为约束满足问题，具体代码如代码清单3-16所示。

代码清单3-16　send_more_money.py

```c
from csp import Constraint, CSP
from typing import Dict, List, Optional
class SendMoreMoneyConstraint(Constraint[str, int]):
    def __init__(self, letters: List[str]) -> None:
       super().__init__(letters)
       self.letters: List[str] = letters
    def satisfied(self, assignment: Dict[str, int]) -> bool:
        # if there are duplicate values, then it's not a solution
        if len(set(assignment.values())) < len(assignment):
            return False
        # if all variables have been assigned, check if it adds correctly
        if len(assignment) == len(self.letters):
            s: int = assignment["S"]
            e: int = assignment["E"]
            n: int = assignment["N"]
            d: int = assignment["D"]
            m: int = assignment["M"]
            o: int = assignment["O"]
            r: int = assignment["R"]
            y: int = assignment["Y"]
            send: int = s * 1000 + e * 100 + n * 10 + d
            more: int = m * 1000 + o * 100 + r * 10 + e
            money: int = m * 10000 + o * 1000 + n * 100 + e * 10 + y
            return send + more == money
        return True # no conflict

```

`SendMoreMoneyConstraint` 的 `satisfied()` 方法完成了一些任务。首先，它检查是否存在多个字母代表同一个数字的情况，如果存在则说明那是一个无效解，返回 `False` 。然后，它检查是否已给所有字母赋值，如果是则会检查已有赋值是否符合公式（SEND+MORE=MONEY），如果符合则说明解已找到，返回 `True` ，否则返回 `False` 。最后，如果尚未给所有字母赋值，则返回 `True` ，这是为了保证能继续求解。

下面试着运行一下代码清单3-17中的代码。

代码清单3-17　send_more_money.py（续）

```c
if __name__ == "__main__":
    letters: List[str] = ["S", "E", "N", "D", "M", "O", "R", "Y"]
    possible_digits: Dict[str, List[int]] = {}
    for letter in letters:
        possible_digits[letter] = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    possible_digits["M"] = [1]  # so we don't get answers starting with a 0
    csp: CSP[str, int] = CSP(letters, possible_digits)
    csp.add_constraint(SendMoreMoneyConstraint(letters))
    solution: Optional[Dict[str, int]] = csp.backtracking_search()
    if solution is None:
        print("No solution found!")
    else:
        print(solution)

```

注意，这里会预先给字母M赋上答案，这是为了确保M的解中不会包含0，因为约束里没有规定数字不能从0开始。大家可以去试试，看看不做此预先赋值会发生什么情况。

结果将如下所示：

```c
{'S': 9, 'E': 5, 'N': 6, 'D': 7, 'M': 1, 'O': 0, 'R': 8, 'Y': 2}
```

