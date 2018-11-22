#Let's Build A Simple Interpreter
  
>If  you learn only methods, you'll be tied to your methods. But if you learn principles, you can devise your own methods.  

---
基础术语
编译器（compiler）：language --> machine language  
解释器（interpreter）: language --> some other forms but not machine language
  
***一句话说明，到中间语言还是直接到机器语言***      
  
---
词法分析器（lexical analyzer）
- token, a token is an object that has a type and a value  
- lexeme, a lexeme is a sequence of characters that form a token, like instance of token    
- lexical analyzer is used to breaking the input strings into tokens    
  
***一句话概括，找出所有标记***    
  
![example](https://ruslanspivak.com/lsbasi-part2/lsbasi_part2_lexemes.png "token & lexeme")  
  
---
解析器（parser）
- the process of finding the structure in the stream of tokens, or put differently, the process of recognizing a phrase in the stream of tokens  
- in the expr method, find 'integer -> op -> integer'    
  
***一句话概括，找出标记中的结构，满足特定约束的结构***  


 
