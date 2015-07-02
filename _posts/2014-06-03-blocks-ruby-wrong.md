---
layout: post
title: "Blocks in Ruby are designed completely wrong"
date: 2014/06/03
categories: ruby
---

Ruby is a great language, and I am completely satisfied with almost all aspects of it. There's one little thing, however, that's just really, *really* annoying.

This is a block:

    puts [*1..5].map{|n| n * n } #=> [1, 4, 9, 16, 25]

This is what the code above is interpreted as by Ruby:

    puts([*1..5].map(){|n| n * n })

This is (one of the many ways) how you would design a `map` function like the built-in one above:

    class WeirdNewArray < Array
      def weird_new_map &block
        new_array = WeirdNewArray.new
        self.each do |el|
          new_array.push block.call(el)
        end
      end
    end

This is how you would design a `double_map` function that would map over an array both forwards and in reverse:

   ???

You see, with the way Ruby's blocks are designed, there is no clean, elegant way to pass multiple blocks to a function.

Let's take a look at another aspect of Ruby: procs. Here are two ways to declare a proc:

    p = proc do |x| x * x; end
    p2 = -> x{ x * x }

Here is how to use that proc:

    puts [*1..5].map(p)

Here is what this whole mess *should* be:

    puts [*1..5].map({|n| n * n }) # passing the block **as a normal argument**
    p = {|n| n * n }
    puts [*1..5].map(p)

Notice a bit of a symmetry here?

    puts [*1..5].map({|n| n * n })
                 p = {|n| n * n }
    puts [*1..5].map(     p      )

Redesigning blocks like this achieves 3 things:

- It is now possible to pass multiple blocks to a function (`f(block1, block2)`)
- No more ugly `->x{}`s littering your code everywhere
- The entire concept of a "block" and all of its special handling is simply removed and replaced with procs, making everything much simpler

Of course, you *could* go even further and get rid of functions entirely:

    # old:
    def f(x); puts x; end
    # new:
    f = {|x| puts x }

That might be stretching it.

Or is it?

Just a little thing to think about.
