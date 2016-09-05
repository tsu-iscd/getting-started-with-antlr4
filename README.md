# Getting Started with ANTLR4

## Installation

`1.` Install Python runtime

```
sudo pip install antlr4-python2-runtime
```

`2.` Install Java (version 1.6 or higher)

```
sudo apt-get install default-jdk
```

`3.` Install `antlr`

Download and copy:

```
$ cd /usr/local/lib
$ curl -O http://www.antlr.org/download/antlr-4.5-complete.jar
$ export CLASSPATH=".:/usr/local/lib/antlr-4.5-complete.jar:$CLASSPATH"
```

Create aliases:

```
$ alias antlr4='java -Xmx500M -cp "/usr/local/lib/antlr-4.5-complete.jar:$CLASSPATH" org.antlr.v4.Tool'
$ alias grun='java org.antlr.v4.runtime.misc.TestRig'
```

## tSQL Example

`1.` Download ANTLR4 [tSQL](https://github.com/antlr/grammars-v4/blob/master/tsql/tsql.g4) grammar.

`2.` Replace `id` to `id_`.

`3`. Create lexer, parser and listener:

```
antlr4 -Dlanguage=Python2 tSQL.g4
```

`4`. Create `sqlparser.py` script:

```
from antlr4 import *
from tSQLLexer import tSQLLexer
from tSQLParser import tSQLParser
from antlr4.tree.Trees import Trees

def main(argv):
    input = FileStream(argv[1])
    lexer = tSQLLexer(input)
    stream = CommonTokenStream(lexer)
    parser = tSQLParser(stream)
    ast = parser.tsql_file()
    print Trees.toStringTree(ast, None, parser)

if __name__ == '__main__':
    main(sys.argv)
```

`5.` Test the parser:

```
python sqlparser.py "SELECT foo FROM bar"
```

## Sources
1. [Getting Started with ANTLR v4](https://github.com/antlr/antlr4/blob/master/doc/getting-started.md)
2. [Getting Started with ANTLR4 in Python](https://github.com/antlr/antlr4/blob/master/doc/python-target.md)
