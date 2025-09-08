#Arithmetic Operations & Functions
In Prolog, we can use arithmetic operations and functions. Here are some examples:

```prolog
?- X is 7 + 3.
X = 10
yes

?- X is 7 - 3.
X = 4
yes

?- X is 7 * 3.
X = 21
yes

?- X is 7 / 3.
X = 2.3333333333333335
yes

?- X is 7 // 3.
X = 2
yes

?- X is 7 mod 3.
X = 1
yes

?- X is 7 rem 3.
X = 1
yes

?- X is 7 ** 3.
X = 343
yes
```



# Cut Operator
Automatic backtracking is one of the most characteristic features of Prolog. But backtracking can lead to inefficiency. Sometimes Prolog can waste time exploring possibilities that lead nowhere. It would be pleasant to have some control over this aspect of its behaviour, but so far we have only seen two (rather crude) ways of doing this: changing rule order, and changing goal order. But there is another way. There is a built-in Prolog predicate ! (the exclamation mark), called cut, which offers a more direct way of exercising control over the way Prolog looks for solutions.

What exactly is cut, and what does it do? It’s simply a special atom that we can use when writing clauses. For example:

```prolog
p(X):- b(X), c(X), !, d(X), e(X).
```

This a perfectly good Prolog rule. As for what cut does, first of all, it is a goal that always succeeds. Second, and more importantly, it has a side effect. Suppose that some goal makes use of this clause (we call this goal the parent goal). Then the cut commits Prolog to any choices that were made since the parent goal was unified with the left hand side of the rule (including, importantly, the choice of using that particular clause). Let’s look at an example to see what this means.

First consider the following piece of cut-free code:

```prolog
p(X):- a(X).

p(X):- b(X), c(X), d(X), e(X).

p(X):- f(X).

a(1).  b(1).   c(1).   d(2).  e(2).  f(3).
       b(2).   c(2).
```

If we pose the query p(X) we will get the following responses:

```prolog
X = 1 ;

X = 2 ;

X = 3 ;
no
```

But now suppose we insert a cut in the second clause:

```prolog
p(X):- b(X), c(X), !, d(X), e(X).
```

if we now pose the query p(X) we will get the following responses:

```prolog
X = 1 ;
no
```



# Lists
As its name suggests, a list is just a plain old list of items. Slightly more precisely, it is a finite sequence of elements. Here are some examples of lists in Prolog:

```prolog
[mia, vincent, jules, yolanda]

[mia, robber(honey_bunny), X, 2, mia]

[]

[mia, [vincent, jules], [butch, girlfriend(butch)]]

[[], dead(z), [2, [b, c]], [], Z, [2, [b, c]]]
```

Prolog has a special built-in operator | which can be used to decompose a list into its head and tail. It is important to get to know how to use | , for it is a key tool for writing Prolog list manipulation programs.

The most obvious use of | is to extract information from lists. We do this by using | together with unification. For example, to get hold of the head and tail of [mia,vincent, jules,yolanda] we can pose the following query:

```prolog
[Head|Tail] = [mia, vincent, jules, yolanda].

Head = mia
Tail = [vincent,jules,yolanda]
yes
```

Empty Lists have no Head and Tail:

```prolog
?- [X|Y] = [].

no
```

We can do a lot more with | ; it really is a flexible tool. For example, suppose we wanted to know what the first two elements of the list were, and also the remainder of the list after the second element. Then we’d pose the following query:

```prolog
?- [X,Y | W] = [[], dead(z), [2, [b, c]], [], Z].

X = []
Y = dead(z)
W = [[2,[b,c]],[],_8327]
Z = _8327
yes
```

That is, the head of the list is bound to X , the second element is bound to Y , and the remainder of the list after the second element is bound to W (that is, W is the list that remains when we take away the first two elements). So | can not only be used to split a list into its head and its tail, we can also use it to split a list at any point. To the left of | we simply indicate how many elements we want to take away from the front of the list, and then to right of the | we will get what remains.

```prolog
?- [X1,X2,X3,X4 | Tail] =
            [[], dead(z), [2, [b, c]], [], Z].

X1 = []
X2 = dead(z)
X3 = [2,[b,c]]
X4 = []
Tail = [_8910]
Z = _8910
yes
```

k, we have got the information we wanted: the values we are interested in are bound to the variables X2 and X4 . But we’ve got a lot of other information too (namely the values bound to X1 , X3 and Tail ). And perhaps we’re not interested in all this other stuff. If so, it’s a bit silly having to explicitly introduce variables X1 , X3 and Tail to deal with it. And in fact, there is a simpler way to obtain only the information we want: we can pose the following query instead:

```prolog
?- [_,X,_,Y|_] = [[], dead(z), [2, [b, c]], [], Z].

X = dead(z)
Y = []
Z = _9593
yes
```

Let’s look at one last example. The third element of our working example is a list (namely [2,  [b,  c]] ). Suppose we wanted to extract the tail of this internal list, and that we are not interested in any other information. How could we do this? As follows:

```prolog
?- [_,_,[_|X]|_] =
      [[], dead(z), [2, [b, c]], [], Z, [2, [b, c]]].

X = [[b,c]]
Z = _10087
yes
```

# Recursion in Lists
 One of the most basic things we would like to know is whether something is an element of a list or not. So let’s write a program that, when given as inputs an arbitrary object X and a list L , tells us whether or not X belongs to L . The program that does this is usually called member , and it is the simplest example of a Prolog program that exploits the recursive structure of lists. Here it is:

```prolog
member(X,[X|T]).
member(X,[H|T]) :- member(X,T).
```

That’s all there is to it: one fact (namely member(X,\[X|T\]) ) and one rule (namely member(X,\[H|T\])  :-  member(X,T) ). But note that the rule is recursive (after all, the functor member occurs in both the rule’s head and body) and it is this that explains why such a short program is all that is required.

# Exercises

## Exercise 1
How will prolog respond to the following queries?

```prolog
[a,b,c,d]  =  [a,[b,c,d]].
[a,b,c,d]  =  [a|[b,c,d]].
[a,b,c,d]  =  [a,b,[c,d]].
[a,b,c,d]  =  [a,b|[c,d]].
[a,b,c,d]  =  [a,b,c,[d]].
[a,b,c,d]  =  [a,b,c|[d]].
[a,b,c,d]  =  [a,b,c,d,[]].
[a,b,c,d]  =  [a,b,c,d|[]].
[]  =  _.
[]  =  [_].
[]  =  [_|[]].
```

## Exercise 2
Write a predicate second(X,List) which checks whether X is the second element of List .

## Exercise 3

Write a predicate swap12(List1,List2) which checks whether List1 is identical to List2 , except that the first two elements are exchanged.

## Exercise 4
 Suppose we are given a knowledge base with the following facts:

 ```prolog
tran(eins,one).
tran(zwei,two).
tran(drei,three).
tran(vier,four).
tran(fuenf,five).
tran(sechs,six).
tran(sieben,seven).
tran(acht,eight).
tran(neun,nine).
```

Write a predicate listtran(G,E) which translates a list of German number words to the corresponding list of English number words. For example:

```prolog
listtran([eins,neun,zwei],X).
```

should give:

```prolog
X = [one,nine,two].
```

Your program should also work in the other direction. For example, if you give it the query:

```prolog
listtran(X,[one,seven,six,two]).
```

it should return:

```prolog
X = [eins,sieben,sechs,zwei].
```

## Exercise 5
Write a predicate twice(In,Out) whose left argument is a list, and whose right argument is a list consisting of every element in the left list written twice. For example, the query:

```prolog
twice([a,4,buggle],X).
```

should return:

```prolog
X = [a,a,4,4,buggle,buggle].
```
And the query

```prolog
twice([1,2,1,1],X).
```

should return:

```prolog
X = [1,1,2,2,1,1,1,1].
```

## Exercise 6
Draw the search trees for the following three queries:

```prolog
member(a,[c,b,a,y]).
member(x,[c,b,a,y]).
member(a,[c,b,a,y,a]).
```

