---
title: "プログラミング言語Shenのざっくりした紹介"
emoji: "👻"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [lisp]
published: true 
---

この記事はまだ未完成です。
何回かにわけて記事を書いていきます。

# プログラミング言語Shenのざっくりした紹介

ShenはLispの方言の1つで静的な型付けShenは強力な型システムや、関数型プログラミング言語をサポートしています。

## FEATURES

### PATTERN MATCHING

```lisp
(define filter
  _ []       -> []
  F [X | Xs] -> [X | (filter F Xs)] where (F X)
  F [_ | Xs] -> (filter F Xs))
```

```lisp
(define element?
  _ []      -> false
  X [X | _] -> true
  X [_ | Y] -> (element? X Y))
``` 
### BACKTRACKING


```lisp
(define walk
  _ []      <- (fail)
  F [X | _] -> X where (F X)
  F [_ | Y] -> (walk F Y))
``` 

### LAMBDA CALCULUS CONSISTENCY

```lisp
(define y-combinator
  F -> ((/. X (X X))
        (/. X (F (/. Y ((X X) Y))))))
```

### LAZY EVALUTION

```lisp
(let F (freeze (output "Hello!"))
  (thaw F))
```

> "Hello!"

### OPTIONAL TYPE CHECKING


```lisp
(tc +)

(define map
  {(A --> B) --> (list A) --> (list B)}
  _ []       -> []
  F [X | Xs] -> [(F X) | (map F Xs)])

(map (+ 1) ["a" "b" "c"])
```

> type error

### CONFIGURABLE TYPE RULES


```lisp
(datatype maybe-type

  _____________________
    none : (maybe A);

         X : A;
  _____________________
  (some X) : (maybe A);

      M : (maybe A);
  _____________________
     (unwrap M) : A;)
```

### INTEGRATED LOGIC ENGINE

```lisp
(defprolog member
  X [X | _] <-- ;
  X [_ | Y] <-- (member X Y);)

(prolog?
  (member X [1 2 3])
  (member X [3 4 5])
  (return X))
```

> 3

### BUILT-IN COMPILER-COMPILER

```lisp
(define bit?
  B -> (element? B [0 1]))

(defcc <b>
  B <b> := [B | <b>] where (bit? B);
  B     := [B] where (bit? B);)
```

### UNIQUE MACROS


```lisp
(defmacro infix-macro
  [X + Y] -> [+ X Y]
  [X * Y] -> [* X Y])
```