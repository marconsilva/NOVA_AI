# Hello World
Run the SWI-Prolog interpreter and type the following command:
```prolog
write('Hello World').
```

Note − After each line, you have to use one period (.) symbol to show that the line has ended.

When you run the above program, you will get the following output:
```prolog
Hello World
true
```

Now let us see how to run the Prolog script file (extension is *.pl) into the Prolog console.

first create a file named helloworld.pl and write the following code:
```prolog
main :- write('This is sample Prolog program'),
write(' This program is written into hello_world.pl file').
```
Before running *.pl file, we must change the directory to the location where the file is saved. To change the directory, use the following command:
```prolog
cd('C:/Users/your_directory_path').
```

Now you can run the Prolog script file using the following command:
```prolog
consult('helloworld.pl').
```

When you run the above command, you will get the following output:
```prolog
true
```

Finally you can run the following command to execute the script file:
```prolog
main.
```

When you run the above command, you will get the following output:
```prolog
This is sample Prolog program This program is written into hello_world.pl file
true.
```

# Basics - Facts, Rules, and Queries
In Prolog, we can define facts, rules, and queries. Let us see how to define facts, rules, and queries in Prolog.

## Facts
Facts are the statements that provide some information about the domain. Facts are used to define the properties of the objects. Facts are defined using the following syntax:

```prolog
likes(mary, apple).
likes(mary, pear).
likes(john, pear).
likes(john, mary).
```

In the above example, we have defined the likes facts. The first fact says that Mary likes apple, the second fact says that Mary likes pear, the third fact says that John likes pear, and the fourth fact says that John likes Mary.

## Rules

Rules are the statements that define the relationship between the objects. Rules are defined using the following syntax:

```prolog
likes(john, X) :- likes(X, apple).
```

In the above example, we have defined the rule. The rule says that John likes X if X likes apple.

## Queries

Queries are the statements that ask the Prolog interpreter to find the solution. Queries are defined using the following syntax:

```prolog
likes(john, X).
```

In the above example, we have defined the query. The query says that find the value of X such that John likes X.

Lets see this with an example. Create knowlage base into a file named kb1.pl and write the following code:
```prolog
girl(priya).
girl(tiyasha).
girl(jaya).
can_cook(priya).
```

Now we can use this knowledge base by posing some queries. “Is priya a girl?”, it will reply “yes”, “is jamini a girl?” then it will answer “No”, because it does not know who jamini is. Our next question is “Can Priya cook?”, it will say “yes”, but if we ask the same question for Jaya, it will say “No”.

Compile the file and run the following queries:
```prolog
consult('kb1.pl').

girl(priya).

can_cook(priya).

can_cook(jaya).

```

Let us see another knowledge base, where we have some rules. Rules contain some information that are conditionally true about the domain of interest. Suppose our knowledge base is as follows:
```prolog
sing_a_song(ananya).
listens_to_music(rohit).

listens_to_music(ananya) :- sing_a_song(ananya).
happy(ananya) :- sing_a_song(ananya).
happy(rohit) :- listens_to_music(rohit).
playes_guitar(rohit) :- listens_to_music(rohit).
```

Now lets pose some queries to the knowledge base. Compile the file and run the following queries:
```prolog
consult('kb2.pl').

happy(rohit).

sing_a_song(rohit).

sing_a_song(ananya).

playes_guitar(rohit).

playes_guitar(ananya).

listens_to_music(ananya).
```

# Variables
In Prolog, variables are used to represent the unknown values. Variables always start with uppercase, and are defined using the following syntax:

```prolog
likes(john, X).
```

Lets create a file named kb3.pl and write the following code:
```prolog
can_cook(priya).
can_cook(jaya).
can_cook(tiyasha).

likes(priya,jaya) :- can_cook(jaya).
likes(priya,tiyasha) :- can_cook(tiyasha).
```

Now we can pose some queries to the knowledge base. Compile the file and run the following queries:
```prolog
consult('kb3.pl').

can_cook(X).

likes(priya,X).
```

On the above examples we have seen how to use variables in Prolog. In the first query, we have asked the Prolog interpreter to find the value of X such that X can cook. If we press enter, then it will come out, otherwise if we press semicolon (;), then it will show the next result.

In the second query, we have asked the Prolog interpreter to find the value of X such that Priya likes X.

# Relations
In Prolog, relations are used to define the relationship between the objects. 

Imagine that we want the concept of brothers. we can define it as follows:

- They both are male.
- They have the same parent.

```prolog
parent(sudip, piyus).
parent(sudip, raj).
male(piyus).
male(raj).
brother(X,Y) :- parent(Z,X), parent(Z,Y),male(X), male(Y)
```

Lets create a file named kb4.pl and write the following code:
```prolog
female(pam).
female(liz).
female(pat).
female(ann).
male(jim).
male(bob).
male(tom).
male(peter).
parent(pam,bob).
parent(tom,bob).
parent(tom,liz).
parent(bob,ann).
parent(bob,pat).
parent(pat,jim).
parent(bob,peter).
parent(peter,jim).
mother(X,Y):- parent(X,Y),female(X).
father(X,Y):- parent(X,Y),male(X).
haschild(X):- parent(X,_).
sister(X,Y):- parent(Z,X),parent(Z,Y),female(X),X\==Y.
brother(X,Y):-parent(Z,X),parent(Z,Y),male(X),X\==Y.
```

now we can compile and query this family tree. Compile the file and run the following queries:
```prolog
consult('kb4.pl').

parent(X,jim).

mother(X,Y).

haschild(X).

sister(X,Y).

brother(X,Y).
```

Note that the symbol \== is used to denote not equal to.
Note also that the underscore (_) is used to denote an anonymous variable, represents an argument whose specific value is irrelevant.

for example in the above knowledge base, the query haschild(X) will return all the facts for parent X of someaone.

Lets extend the knowledge base with the following code and create a file named kb5.pl:
```prolog
female(pam).
female(liz).
female(pat).
female(ann).

male(jim).
male(bob).
male(tom).
male(peter).

parent(pam,bob).
parent(tom,bob).
parent(tom,liz).
parent(bob,ann).

parent(bob,pat).
parent(pat,jim).
parent(bob,peter).
parent(peter,jim).

mother(X,Y):- parent(X,Y),female(X).
father(X,Y):-parent(X,Y),male(X).
sister(X,Y):-parent(Z,X),parent(Z,Y),female(X),X\==Y.
brother(X,Y):-parent(Z,X),parent(Z,Y),male(X),X\==Y.
grandparent(X,Y):-parent(X,Z),parent(Z,Y).
grandmother(X,Z):-mother(X,Y),parent(Y,Z).
grandfather(X,Z):-father(X,Y),parent(Y,Z).
wife(X,Y):-parent(X,Z),parent(Y,Z),female(X),male(Y).
uncle(X,Z):-brother(X,Y),parent(Y,Z).
```

Now he have relationships between grandparent, grandmother, grandfather, wife and uncle. Compile the file and run the following queries:
```prolog
consult('kb5.pl').

uncle(X,Y).
grandparent(X,Y).
wife(X,Y).
```

## Trace
In Prolog, trace is used to show the execution of the program. It shows the execution of the program step by step. To enable the trace, use the following command:

```prolog
mother(X,Y).

trace.
```

When you run the above command, you will get the following output:
```prolog
[trace]  
| ?- mother(pam,Y).
   1 1 Call: mother(pam,_23) ?
   2 2 Call: parent(pam,_23) ?
   2 2 Exit: parent(pam,bob) ?
   3 2 Call: female(pam) ?
   3 2 Exit: female(pam) ?
   1 1 Exit: mother(pam,bob) ?

Y = bob
    
(16 ms) yes
```

To disable the trace, use the following command:

```prolog
notrace.
```

## Recursion

In Prolog, recursion is used to define the rules that call themselves. Recursion is used to solve the complex problems by dividing it into smaller problems. Let us see how to define the recursive rules in Prolog.

for example:
```prolog

predecessor(X, Z) :- parent(X, Z).
predecessor(X, Z) :- parent(X, Y),predecessor(Y, Z).
```

Lets create a new file named kb6.pl and write the following code:
```prolog
female(pam).
female(liz).
female(pat).
female(ann).

male(jim).
male(bob).
male(tom).
male(peter).

parent(pam,bob).
parent(tom,bob).
parent(tom,liz).
parent(bob,ann).
parent(bob,pat).
parent(pat,jim).
parent(bob,peter).
parent(peter,jim).

predecessor(X, Z) :- parent(X, Z).
predecessor(X, Z) :- parent(X, Y),predecessor(Y, Z).
```

Lets compile the file and run the following queries and do some tracing:
```prolog
consult('kb7.pl').

predecessor(peter,X).

trace.
```

When you run the above command, you will get the following output:
```prolog
{trace}
| ?- predecessor(bob,X).
   1 1 Call: predecessor(bob,_23) ?
   2 2 Call: parent(bob,_23) ?
   2 2 Exit: parent(bob,ann) ?
   1 1 Exit: predecessor(bob,ann) ?
   
X = ann ? ;
   1 1 Redo: predecessor(bob,ann) ?
   2 2 Redo: parent(bob,ann) ?
   2 2 Exit: parent(bob,pat) ?
   1 1 Exit: predecessor(bob,pat) ?
   
X = pat ? ;
   1 1 Redo: predecessor(bob,pat) ?
   2 2 Redo: parent(bob,pat) ?
   2 2 Exit: parent(bob,peter) ?
   1 1 Exit: predecessor(bob,peter) ?
   
X = peter ? ;
   1 1 Redo: predecessor(bob,peter) ?
   2 2 Call: parent(bob,_92) ?
   2 2 Exit: parent(bob,ann) ?
   3 2 Call: predecessor(ann,_23) ?
   4 3 Call: parent(ann,_23) ?
   4 3 Fail: parent(ann,_23) ?
   4 3 Call: parent(ann,_141) ?
   4 3 Fail: parent(ann,_129) ?
   3 2 Fail: predecessor(ann,_23) ?
   2 2 Redo: parent(bob,ann) ?
   2 2 Exit: parent(bob,pat) ?
   3 2 Call: predecessor(pat,_23) ?
   4 3 Call: parent(pat,_23) ?
   4 3 Exit: parent(pat,jim) ?
   3 2 Exit: predecessor(pat,jim) ?
   1 1 Exit: predecessor(bob,jim) ?
   
X = jim ? ;
   1 1 Redo: predecessor(bob,jim) ?
   3 2 Redo: predecessor(pat,jim) ?
   4 3 Call: parent(pat,_141) ?
   4 3 Exit: parent(pat,jim) ?
   5 3 Call: predecessor(jim,_23) ?
   6 4 Call: parent(jim,_23) ?
   6 4 Fail: parent(jim,_23) ?
   6 4 Call: parent(jim,_190) ?
   6 4 Fail: parent(jim,_178) ?
   5 3 Fail: predecessor(jim,_23) ?
   3 2 Fail: predecessor(pat,_23) ?
   2 2 Redo: parent(bob,pat) ?
   2 2 Exit: parent(bob,peter) ?
   3 2 Call: predecessor(peter,_23) ?
   4 3 Call: parent(peter,_23) ?
   4 3 Exit: parent(peter,jim) ?
   3 2 Exit: predecessor(peter,jim) ?
   1 1 Exit: predecessor(bob,jim) ?
   
X = jim ?

(78 ms) yes

```

