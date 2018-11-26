#Let's Build A Simple Interpreter
  
>If  you learn only methods, you'll be tied to your methods. But if you learn principles, you can devise your own methods.  


##Source code for the series **Let's Build A Simple Interpreter**

+ [Let's Build A Simple Interpreter. Part 1.](https://ruslanspivak.com/lsbasi-part1/)
+ [Let's Build A Simple Interpreter. Part 2.](https://ruslanspivak.com/lsbasi-part2/)
+ [Let's Build A Simple Interpreter. Part 3.](https://ruslanspivak.com/lsbasi-part3/)
+ [Let's Build A Simple Interpreter. Part 4.](https://ruslanspivak.com/lsbasi-part4/)
+ [Let's Build A Simple Interpreter. Part 5.](https://ruslanspivak.com/lsbasi-part5/)
+ [Let's Build A Simple Interpreter. Part 6.](https://ruslanspivak.com/lsbasi-part6/)
+ [Let's Build A Simple Interpreter. Part 7.](https://ruslanspivak.com/lsbasi-part7/)
+ [Let's Build A Simple Interpreter. Part 8.](https://ruslanspivak.com/lsbasi-part8/)
+ [Let's Build A Simple Interpreter. Part 9.](https://ruslanspivak.com/lsbasi-part9/)
+ [Let's Build A Simple Interpreter. Part 10.](https://ruslanspivak.com/lsbasi-part10/)
+ [Let's Build A Simple Interpreter. Part 11.](https://ruslanspivak.com/lsbasi-part11/)
+ [Let's Build A Simple Interpreter. Part 12.](https://ruslanspivak.com/lsbasi-part12/)
+ [Let's Build A Simple Interpreter. Part 13.](https://ruslanspivak.com/lsbasi-part13/)
+ [Let's Build A Simple Interpreter. Part 14.](https://ruslanspivak.com/lsbasi-part14/)



##基础术语   
编译器（compiler）：language --> machine language  
解释器（interpreter）: language --> some other forms but not machine language
  
***一句话说明，到中间语言还是直接到机器语言***      
  

##**词法分析器（lexical analyzer）**  
- token, a token is an object that has a type and a value  
- lexeme, a lexeme is a sequence of characters that form a token, like instance of token    
- lexical analyzer is used to breaking the input strings into tokens    
  
***一句话概括，找出所有标记***    
  
![example](https://ruslanspivak.com/lsbasi-part2/lsbasi_part2_lexemes.png "token & lexeme")  
  

##解析器（parser）
- the process of finding the structure in the stream of tokens, or put differently, the process of recognizing a phrase in the stream of tokens  
- in the expr method, find 'integer -> op -> integer'    
  
***一句话概括，找出标记中的结构，满足特定约束的结构*** 

##语法图（syntax diagram）
- A syntax diagram is a graphical representation of a programming language's syntax rules.  
- Syntax diagrams serve two main purposes:  
   -  They graphically represent the specification(grammar) of a programming language.
   -  They can be used to help you write parser - you can map a diagram to code by following simple rules.  
- Parsing is also called syntax analysis, and the parser is also aptly called, a syntax analyzer. 解析也被称为语法分析，同理，解析器被称为语法分析器   

![example](https://ruslanspivak.com/lsbasi-part3/lsbasi_part3_syntax_diagram.png "expr'syntax diagram ")    

***一句话概括，解析或语法解析就是把语法图用代码实现一遍***

##上下文无关语法（Context-free grammars）

from wiki
>In formal language theory, a context-free grammar(CFG) is a certain type of formal grammar: a set of production rules that describe all possible strings in a given formal language. Productions rules are simple replacements.   
   
上下文无关语法是一种形式语法，以一种给定的形式语描述生成规则，然后通过一组生成规则描述所有可能的字符串。在解释器的例子中，这种形式语言的写法与正则表达式非常类似。
   
For example, the rule:  
>A --> alfa   
>A --> beta.  
means that A can be replaced with either alfa or beta.  
  
In context-free grammars, all rules are one-to-one, one-to-many, or one-to-none. These rules can be applied regardless of context.  
The left-hand side of the production rule is always a **nonterminal** symbol. This means that *the symbol does not appear in the resulting formal language*.我理解其实就是一个标记，类似规则名或变量名之类的东西。      

simple expr‘s formal representation:   
>expr : factor((plus | minus)factor))*    
>factor: integer   
>notes: * means one-to-many

##关联性与优先级（associativity and precedence）    
如何根据优先级构造语法规则？  

- 对于每个优先级构造一个non-terminal。 non-terminal的body应包含该优先级的算数运算符和更高一级优先级的non-terminal   
- 为原子粒度的表达式创建一个额外的non-termianl factor，在这里的例子，是integer。所以，创建的规则即为，如果你有N级优先级，那么你需要N+1级non-terminal。

Example -- surpport mul and div:  
>expr : term( (plus | minus) term) *   
>term : factor( (mul | div) factor) *     
>factor : integer     
  
***一句话概括，将某一优先级的计算封装为一non-terminal，上一优先级只是对低一级non-terminal的计算，然后递归*** 
