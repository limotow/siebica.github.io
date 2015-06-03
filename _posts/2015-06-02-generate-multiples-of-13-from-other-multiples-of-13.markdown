---
layout: post
title:  "Generating Multiples of 13"
date:   2015-06-02 10:08:00
categories: math primes
---
In the times when I was still superstitious I was playing around with the number 13 and came up with a formula to get a new multiple of 13 from an existing multiple of 13. The process of how to do it is described below.

Given a number __m__ = a<sub>0</sub> + a<sub>1</sub> * 10 + a<sub>2</sub> * 10<sup>2</sup> + ... + a<sub>m</sub> * 10<sup>m</sup> that is a _M<sub>13</sub>_ (i.e. m mod 13 = 0), you can apply the following formula to it and get another number __n__ that is also a _M<sub>13</sub>_:  
__n__ = 2 * ( a<sub>m</sub> + a<sub>m-1</sub> * 10 + a<sub>m-2</sub> * 10<sup>2</sup> + ... + a<sub>0</sub> * 10<sup>m</sup>) + 2 * ( a<sub>1</sub> + a<sub>2</sub> - a<sub>4</sub> - a<sub>5</sub> + a<sub>7</sub> + a<sub>8</sub> - ... )

The code below - written in Ruby - gets the corresponding __n__ number from an initial __m__ number:  
{% highlight ruby %}
FACTOR = 13

def getNewMultiple(initial)
  result = 2 * initial.to_s.reverse.to_i

  sign = -1
  initial.to_s.each_char.each_with_index do |char, index|
    if index % 3 == 0
      sign = -sign
      next
    end
    result += sign * char.to_i
  end

  raise "#{result} is not multiple of #{FACTOR}" if result % FACTOR > 0
  result
end
{% endhighlight %}
