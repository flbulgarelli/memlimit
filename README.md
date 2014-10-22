# memlimit

```memlimit``` is a damn simple script for making a virtual-memory limited version of any other command. 

¿Why would you need that? Well, in my case I frequently use interactive programming shells/interpreters/tools. And it is not uncommon to run by mistake an expression or command that is memory consuming. This is particulary true when I work with functional-like languages, and you mess lazy and eager evaluations.  

If you are running, say, a JVM contained shell this is not usually a problem, since JVM imposes memory limits to what is run inside. 

But other interpreters will by default ask for more memory to your OS until it eventually gets filled and masive swapping starts. If this happens quickly you may not have time to abort the memory hungry command. Its is not funny when that happens, bro.  

# Some samples you SHOULD NOT run

Using ```ghci```: 

```haskell
sum [1..]
```

(Ouch, sum is not implemented with foldl')

Using ```erl```:

```erlang
lists:duplicate(10000000, 3).
```

(Ouch, forgot duplicate is not lazy)

Perhaps those examples seems contrived, but it is easy to get into them through a typo or more complex code. 

# Usage

```bash
alias YOUR_COMMAND = "memlimit MAX_SIZE YOUR_COMMAND"
```

# Example

Limiting ```ghci``` limit to 1GiB - it will crash if such limit is exceeded:

```bash
alias ghci="memlimit 1024 ghci"
```

# FAQ 

## Why just not use a global memory limit?

Becasue I want to only limit certain commands. 

## How does it work?

It simply opens a new shell in the context of ```ulimint```

## Caveats

```memlimit``` does not work as expected if memlimited process forks themself. If you need a true black-box memory or time limit, consider using something like https://github.com/pshved/timeout
