<p align="center">
  <a href="https://typer.tiangolo.com"><img src="https://typer.tiangolo.com/img/logo-margin/logo-margin-vector.svg#only-light" alt="Typer"></a>

</p>
<p align="center">
    <em>Typer，构建出色的命令行程序。编写轻松。基于 Python 类型注解。</em>
</p>
<p align="center">
<a href="https://github.com/fastapi/typer/actions?query=workflow%3ATest+event%3Apush+branch%3Amaster">
    <img src="https://github.com/fastapi/typer/actions/workflows/test.yml/badge.svg?event=push&branch=master" alt="Test">
</a>
<a href="https://coverage-badge.samuelcolvin.workers.dev/redirect/fastapi/typer">
    <img src="https://coverage-badge.samuelcolvin.workers.dev/fastapi/typer.svg" alt="Coverage">
<a href="https://pypi.org/project/typer">
    <img src="https://img.shields.io/pypi/v/typer?color=%2334D058&label=pypi%20package" alt="Package version">
</a>
</p>

---

**文档**：[https://typer.tiangolo.com](https://typer.tiangolo.com)

**源代码**：[https://github.com/fastapi/typer](https://github.com/fastapi/typer)

---

Typer 是一个用于构建 <abbr title="command line interface，即从终端执行的命令行程序">CLI</abbr>（命令行程序）的库，让用户**喜欢使用**、开发者**喜欢创建**。它基于 Python 类型注解。

它同时也是一个命令行工具，可用于运行脚本，并自动将其转换成 CLI 程序。

其主要特性包括：

* **编写直观**：出色的编辑器支持。到处都有<abbr title="也称为自动补全、autocompletion、IntelliSense">补全</abbr>。减少调试时间。专为易用、易学而设计。少花时间阅读文档。
* **使用方便**：对最终用户来说非常易用。自动生成帮助信息，并为所有 Shell 提供自动补全。
* **精简**：最大限度减少代码重复。每个参数声明即可获得多项功能。更少 Bug。
* **起步简单**：最简单的示例在你的应用中只需增加 2 行代码：**1 个 import，1 次函数调用**。
* **规模可扩展**：可以任意扩展复杂度，创建任意复杂的命令树和子命令组，并支持选项和参数。
* **运行脚本**：Typer 内置了一个 `typer` 命令 / 程序，可用于运行脚本，自动将其转换成 CLI 程序，即便脚本内部并未使用 Typer。

## 命令行程序界的 FastAPI

**Typer** 是 [FastAPI](https://fastapi.tiangolo.com) 的小兄弟，它是命令行程序界的 FastAPI。

## 安装

创建并激活一个 [虚拟环境](https://typer.tiangolo.com/virtual-environments/)，然后安装 **Typer**：

<div class="termy">

```console
$ pip install typer
---> 100%
Successfully installed typer rich shellingham
```

</div>

## 示例

### 最简示例

* 创建一个文件 `main.py`，内容如下：

```Python
def main(name: str):
    print(f"Hello {name}")
```

这个脚本内部甚至都没有使用 Typer。但你可以用 `typer` 命令把它当作一个 CLI 程序来运行。

### 运行它

用 `typer` 命令运行你的程序：

<div class="termy">

```console
// 运行你的程序
$ typer main.py run

// 你会得到一个友好的错误提示：你漏掉了 'name'
Usage: typer [PATH_OR_MODULE] run [OPTIONS] {name}
Try 'typer [PATH_OR_MODULE] run --help' for help.
╭─ Error ───────────────────────────────────────────╮
│ Missing argument 'name'.                          │
╰───────────────────────────────────────────────────╯


// 自动获得 --help 帮助信息
$ typer main.py run --help

Usage: typer [PATH_OR_MODULE] run [OPTIONS] {name}

Run the provided Typer app.

╭─ Arguments ───────────────────────────────────────╮
│ *    name      <str>  [required]                  │
╰───────────────────────────────────────────────────╯
╭─ Options ─────────────────────────────────────────╮
│ --help          Show this message and exit.       │
╰───────────────────────────────────────────────────╯

// 现在传入 'name' 参数
$ typer main.py run Camila

Hello Camila

// 成功运行！🎉
```

</div>

这是最简单的使用场景，内部甚至没有用到 Typer，但对于简单脚本来说已经相当有用。

**注意**：当你创建一个 Python 包并用 `--install-completion` 运行，或使用 `typer` 命令时，自动补全才会生效。

## 在你的代码中使用 Typer

现在让我们开始在自己的代码中使用 Typer，将 `main.py` 更新为：

```Python
import typer


def main(name: str):
    print(f"Hello {name}")


if __name__ == "__main__":
    typer.run(main)
```

现在你可以直接用 Python 运行它：

<div class="termy">

```console
// 运行你的程序
$ python main.py

// 你会得到一个友好的错误提示：你漏掉了 'name'
Usage: main.py [OPTIONS] {name}
Try 'main.py --help' for help.
╭─ Error ───────────────────────────────────────────╮
│ Missing argument 'name'.                          │
╰───────────────────────────────────────────────────╯


// 自动获得 --help 帮助信息
$ python main.py --help

Usage: main.py [OPTIONS] {name}

╭─ Arguments ───────────────────────────────────────╮
│ *    name      <str>  [required]                  │
╰───────────────────────────────────────────────────╯
╭─ Options ─────────────────────────────────────────╮
│ --help          Show this message and exit.       │
╰───────────────────────────────────────────────────╯

// 现在传入 'name' 参数
$ python main.py Camila

Hello Camila

// 成功运行！🎉
```

</div>

**注意**：你也可以用 `typer` 命令来调用这个脚本，但并非必须。

## 进阶示例

这是尽可能简单的示例。

现在让我们看一个稍微复杂一点的例子。

### 包含两个子命令的示例

修改文件 `main.py`。

创建一个 `typer.Typer()` 应用，并创建两个带有各自参数的子命令。

```Python hl_lines="3  6  11  20"
import typer

app = typer.Typer()


@app.command()
def hello(name: str):
    print(f"Hello {name}")


@app.command()
def goodbye(name: str, formal: bool = False):
    if formal:
        print(f"Goodbye Ms. {name}. Have a good day.")
    else:
        print(f"Bye {name}!")


if __name__ == "__main__":
    app()
```

这样做会：

* 显式创建一个 `typer.Typer` 应用。
    * 之前使用的 `typer.run` 实际上会为你隐式创建一个。
* 用 `@app.command()` 添加两个子命令。
* 直接执行 `app()` 本身，就像调用一个函数一样（而不是使用 `typer.run`）。

### 运行进阶示例

查看新的帮助信息：

<div class="termy">

```console
$ python main.py --help

 Usage: main.py [OPTIONS] COMMAND [ARGS]...

╭─ Options ─────────────────────────────────────────╮
│ --install-completion          Install completion  │
│                               for the current     │
│                               shell.              │
│ --show-completion             Show completion for │
│                               the current shell,  │
│                               to copy it or       │
│                               customize the       │
│                               installation.       │
│ --help                        Show this message   │
│                               and exit.           │
╰───────────────────────────────────────────────────╯
╭─ Commands ────────────────────────────────────────╮
│ hello                                             │
│ goodbye                                           │
╰───────────────────────────────────────────────────╯

// 当你创建一个包时，将免费获得 ✨ 自动补全 ✨，通过 --install-completion 安装

// 你有两个子命令（即两个函数）：hello 和 goodbye
```

</div>

现在查看 `hello` 命令的帮助信息：

<div class="termy">

```console
$ python main.py hello --help

 Usage: main.py hello [OPTIONS] {name}

╭─ Arguments ───────────────────────────────────────╮
│ *    name      <str>  [required]                  │
╰───────────────────────────────────────────────────╯
╭─ Options ─────────────────────────────────────────╮
│ --help          Show this message and exit.       │
╰───────────────────────────────────────────────────╯
```

</div>

现在查看 `goodbye` 命令的帮助信息：

<div class="termy">

```console
$ python main.py goodbye --help

 Usage: main.py goodbye [OPTIONS] {name}

╭─ Arguments ───────────────────────────────────────╮
│ *    name      <str>  [required]                  │
╰───────────────────────────────────────────────────╯
╭─ Options ─────────────────────────────────────────╮
│ --formal    --no-formal      [default: no-formal] │
│ --help                       Show this message    │
│                              and exit.            │
╰───────────────────────────────────────────────────╯

// 为 bool 选项自动生成 --formal 和 --no-formal 🎉
```

</div>

现在你可以试一下这个新的命令行程序：

<div class="termy">

```console
// 使用 hello 命令

$ python main.py hello Camila

Hello Camila

// 使用 goodbye 命令

$ python main.py goodbye Camila

Bye Camila!

// 加上 --formal

$ python main.py goodbye --formal Camila

Goodbye Ms. Camila. Have a good day.
```

</div>

**注意**：如果你的程序只有一个命令，默认情况下命令名在用法中会被**省略**：`python main.py Camila`。但当存在多个命令时，你必须**显式地写上命令名**：`python main.py hello Camila`。详见 [单命令还是多命令](https://typer.tiangolo.com/tutorial/commands/one-or-multiple/)。

### 小结

总之，你只需**声明一次**参数的类型（*CLI 参数* 和 *CLI 选项*），将其作为函数参数即可。

你使用的是标准的现代 Python 类型。

你不需要学习新的语法、某个特定库的方法或类等等。

只需标准的 **Python**。

例如，对于 `int`：

```Python
total: int
```

或对于 `bool` 标志：

```Python
force: bool
```

同理也适用于**文件**、**路径**、**枚举**（选项）等。并且还提供了用于创建**子命令组**、添加元数据、额外**校验**等工具。

**你将获得**：出色的编辑器支持，包括无处不在的**补全**和**类型检查**。

**你的用户将获得**：安装你的包或使用 `typer` 命令时，终端（Bash、Zsh、Fish、PowerShell）中的自动 **`--help`** 帮助信息和**自动补全**。

如需包含更多功能的更完整示例，请参阅 <a href="https://typer.tiangolo.com/tutorial/">教程 - 用户指南</a>。

## 依赖项

**Typer** 仅需要少量依赖（大多数都很小）：

* [`rich`](https://rich.readthedocs.io/en/stable/index.html)：用于自动显示格式美观的错误信息。
* [`shellingham`](https://github.com/sarugaku/shellingham)：用于在安装补全时自动检测当前 Shell。
* [`annotated-doc`](https://github.com/fastapi/annotated-doc)：用于从 Python 类型注解生成文档。
* [`colorama`](https://github.com/tartley/colorama)（仅限 Windows）：用于在 Windows 上生成彩色终端文本。

### Click 代码

Typer 过去还依赖 [Click](https://click.palletsprojects.com/)，这是一个用于构建 Python 命令行程序的热门工具。

自 0.26.0 版本起，Typer 已将 Click 内置（vendored，即将 Click 的源代码内部包含进来，而不是作为第三方包安装），并统一了 Typer 与内嵌 Click 源代码之间的交互，以便未来更易于维护。

请注意，随着我们持续改进和扩展 Typer 的代码库，部分 Click 功能在未来将不再可用。

### `typer-slim`

曾经有一个名为 `typer-slim` 的精简版 Typer，它不包含 `rich` 和 `shellingham` 这两个依赖，也不包含 `typer` 命令。

然而，自 0.22.0 版本起，我们已经停止支持它，`typer-slim` 现在只是安装（完整的）Typer。

如果你想全局禁用 Rich，可以将环境变量 `TYPER_USE_RICH` 设置为 `False` 或 `0`。

## 许可证

本项目基于 MIT 许可证的条款进行授权。
