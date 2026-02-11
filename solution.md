## Solution to Problem 1

(a)

The use of pi in line 4 is bound to the declared value of pi from line 3 while pi in line 7 is bound to the declaration of pi at line 1. The compiler should check if in its own scope, otherwise default to whichever value matches it first (looking locally first, then going outward towards global scope).

(b)

The use of x at line 3 is bound by the parameter x in the function f, while lines 6 and 10 are bound to the defined case x. The use of x at line 11 is bound by the declaration of x at line 1. This is once again to do with the way scope is checked.

## Solution to Problem 2

(a) Execution trace:

```
pow(2,3): if 3 > 0 then 2*pow(2,2) else 1
          if __true__ then __2*pow(2,2)__ else 1
    = 2*pow(2,2)
    pow(2,2): if 2 > 0 then 2*pow(2,1) else 1
              if __true__ then __2*pow(2,1)__ else 1
        = 2*2*pow(2,1)
        pow(2,1): if 1 > 0 then 2*pow(2,0) else 1 
                  if __true__ then __2*pow(2,0)__else 1 
            = 2*2*2*pow(2,0)
            pow(2,0): if 0 > 0 then 2*pow(2,-1) else 1
                      if __false__ then __1__
```

(b) Tail-recursive implementation

```
def pow_tail(x:Int, n:Int): Int =
    def pow2(a:Int, b:Int): Int =
        if a<= 0 then b else pow2(a-1,b*x)
    pow2(n,1)

```

Execution trace:

```
pow_tail(2,3): 
    pow2(3,1): if 3 <= 0 then 1 else pow2(2,2)
               if __false__ then __pow2(2,2)__
        pow2(2,2): if 2<=0 then 2 else pow2(1,4)
                   if __false__ then __pow2(1,4)_
            pow(1,4): if 1<=0 then 4 else pow2(0,8)
                      if __false__ then __pow2(0,8)_
                pow(0,8): if 0<=0 then 8 else __pow2(-1,16)__
                          if __true__ then __8__ 
```