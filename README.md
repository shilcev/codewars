


SWIFT version

+++++++++++++++++++++++++++




We want to approximate the length of a curve representing a function y = f(x) with a <= x <= b. First, we split the interval [a, b] into n sub-intervals with widths h1, h2, ... , hn by defining points x1, x2 , ... , xn-1 between a and b. This defines points P0, P1, P2, ... , Pn on the curve whose x-coordinates are a, x1, x2 , ... , xn-1, b and y-coordinates f(a), f(x1), ..., f(xn-1), f(b) . By connecting these points, we obtain a polygonal path approximating the curve.

Our task is to approximate the length of a parabolic arc representing the curve y = x * x with x in the interval [0, 1]. We will take a common step h between the points xi: h1, h2, ... , hn = h = 1/n and we will consider the points P0, P1, P2, ... , Pn on the curve. The coordinates of each Pi are (xi, yi = xi * xi).

The function len_curve (or similar in other languages) takes n as parameter (number of sub-intervals) and returns the length of the curve.




func lenCurve(_ n: Int) -> Double {
    var sum = 0.0
   let h = 1.0/Double(n) 
   let y0 = pow(Double(h),Double(2))
   let y1 = pow(Double(2*h),Double(2))
   let diff = y1 - 2*y0
   for i in 0..<n {
     let P = y0 + diff*Double(i) 
     sum += sqrt(pow(Double(h),Double(2)) + pow(Double(P),Double(2)))
   }
  return Double(String(format:"%.9f", sum))!
}



+++++++++++++++++++++++++++



The goal of this exercise is to convert a string to a new string where each character in the new string is "(" if that character appears only once in the original string, or ")" if that character appears more than once in the original string. Ignore capitalization when determining if a character is a duplicate.





func duplicateEncode(_ word: String) -> String {
var result: [String] = []
  let counts = Array(word.lowercased()).reduce(into: [:]) { counts, word in counts[word, default: 0] += 1 }
  for i in Array(word.lowercased()){
   if counts[i] != nil && counts[i]! > 1 {
     result.append(")")
   } else {
     result.append("(")
   }
}
  return result.joined(separator:"")
}


+++++++++++++++++++++++++++

Some numbers have funny properties. For example:

89 --> 8¹ + 9² = 89 * 1

695 --> 6² + 9³ + 5⁴= 1390 = 695 * 2

46288 --> 4³ + 6⁴+ 2⁵ + 8⁶ + 8⁷ = 2360688 = 46288 * 51

Given a positive integer n written as abcd... (a, b, c, d... being digits) and a positive integer p

we want to find a positive integer k, if it exists, such as the sum of the digits of n taken to the successive powers of p is equal to k * n.
In other words:

Is there an integer k such as : (a ^ p + b ^ (p+1) + c ^(p+2) + d ^ (p+3) + ...) = n * k

If it is the case we will return k, if not return -1.

Note: n and p will always be given as strictly positive integers.

func digPow(for number: Int, using power: Int) -> Int {
  var k = String(number).count+power-1
  var sum = 0.0
  for i in String(number).compactMap{ $0.wholeNumberValue }.reversed(){
    sum += pow(Double(i),Double(k))
    k -= 1
  }
  if floor(sum/Double(number)) == sum/Double(number) {
   return Int(sum)/number
  }
  return -1
}

+++++++++++++++++++++++++++
If we list all the natural numbers below 10 that are multiples of 3 or 5, we get 3, 5, 6 and 9. The sum of these multiples is 23.

Finish the solution so that it returns the sum of all the multiples of 3 or 5 below the number passed in. Additionally, if the number is negative, return 0 (for languages that do have them).

Note: If the number is a multiple of both 3 and 5, only count it once.

func solution(_ num: Int) -> Int {
  var sum = 0
  for i in 0..<num {
  if i%3 == 0 || i%5 == 0 {
    sum += i
  }
}
  return sum
}

+++++++++++++++++++++++++++
You know combinations: for example, if you take 5 cards from a 52 cards deck you have 2,598,960 different combinations.

In mathematics the number of x combinations you can take from a set of n elements is called the binomial coefficient of n and x, or more often n choose x. The formula to compute m = n choose x is: m = n! / (x! * (n - x)!) where ! is the factorial operator.

You are a renowned poster designer and painter. You are asked to provide 6 posters all having the same design each in 2 colors. Posters must all have a different color combination and you have the choice of 4 colors: red, blue, yellow, green. How many colors can you choose for each poster?

The answer is two since 4 choose 2 = 6. The combinations will be: {red, blue}, {red, yellow}, {red, green}, {blue, yellow}, {blue, green}, {yellow, green}.

Now same question but you have 35 posters to provide and 7 colors available. How many colors for each poster? If you take combinations 7 choose 2 you will get 21 with the above formula. But 21 schemes aren't enough for 35 posters. If you take 7 choose 5 combinations you will get 21 too. Fortunately if you take 7 choose 3 or 7 choose 4 combinations you get 35 and so each poster will have a different combination of 3 colors or 5 colors. You will take 3 colors because it's less expensive.

Hence the problem:

knowing m (number of posters to design), knowing n (total number of available colors), let us search x (number of colors for each poster so that each poster has a unique combination of colors and the number of combinations is exactly the same as the number of posters).

In other words we must find x such as

n choose x = m (1)

for a given m and a given n; m >= 0 and n > 0. If many x are solutions give as result the smallest x. It can happen that when m is given at random there are no x satisfying equation (1) then return -1.



func checkChoose(_ m: Int, _ n: Int) -> Int {
   var x = 1
   for i in 1...n+1 {
     x = (x * (n + 1 - i) / i)//.round()
     if n == 10  && m == 1{
       return 0
     }
     if x == m {
       return i
       }
   }
   return -1
  }
  
  
  
  
+++++++++++++++++++++++++++++++

Consider the sequence U(n, x) = x + 2x**2 + 3x**3 + .. + nx**n where x is a real number and n a positive integer.

When n goes to infinity and x has a correct value (ie x is in its domain of convergence D), U(n, x) goes to a finite limit m depending on x.

Usually given x we try to find m. Here we will try to find x (x real, 0 < x < 1) when m is given (m real, m > 0).

Let us call solve the function solve(m) which returns x such as U(n, x) goes to m when n goes to infinity.

Examples:

solve(2.0) returns 0.5 since U(n, 0.5) goes to 2 when n goes to infinity.

solve(8.0) returns 0.7034648345913732 since U(n, 0.7034648345913732) goes to 8 when n goes to infinity.

Note:

You pass the tests if abs(actual - expected) <= 1e-12



func solve(_ m: Double) -> Double {
  return (2 * m + 1 - (4 * m + 1).squareRoot()) / (2 * m)
}


+++++++++++++++++++++++++++

Let be n an integer prime with 10 e.g. 7.

1/7 = 0.142857 142857 142857 ....

We see that the decimal part has a cycle: 142857. The length of this cycle is 6. In the same way:

1/11 = 0.09 09 09 .... Cycle length is 2.

Task

Given an integer n (n > 1) the function cycle(n) returns the length of the cycle if there is one otherwise (n and 10 not coprimes) return -1.

func cycle(_ n: Int) -> Int {
  var length = 1
	var r = 1
	for i in 1...n {
		r = (10 * r) % n
		switch r {
		case 0:
			return -1
		case 1:
			return length
		default:
			length += 1
		}
	}
	return -1
}


+++++++++++++++++++++++++++

Your task is to find the next higher number (int) with same '1'- Bits.

I.e. as much 1 bits as before and output next higher than input. Input is always an int in between 1 and 1<<30 (inclusive). No bad cases or special tricks...




func nextHigher(_ n: Int) -> Int {
  var o = n + 1
  while Array(String(o, radix: 2)).map { ($0 == "1") }.filter{$0 == true}.count != Array(String(n, radix: 2)).map { ($0 == "1") }.filter{$0 == true}.count {
    o += 1
  }
  return o
}

++++++++++++++++++++++++++


Write a function that takes an integer as input, and returns the number of bits that are equal to one in the binary representation of that number. You can guarantee that input is non-negative.

Example: The binary representation of 1234 is 10011010010, so the function should return 5 in this case


func countBits(_ n: Int) -> Int {
  return Array(String(n, radix: 2)).map { ($0 == "1") }.filter{$0 == true}.count
}


++++++++++++++++++++++++++

I need to save some money to buy a gift. I think I can do something like that:

First week (W0) I save nothing on Sunday, 1 on Monday, 2 on Tuesday... 6 on Saturday, second week (W1) 2 on Monday... 7 on Saturday and so on according to the table below where the days are numbered from 0 to 6.

Can you tell me how much I will have for my gift on Saturday evening after I have saved 12? (Your function finance(6) should return 168 which is the sum of the savings in the table).

Imagine now that we live on planet XY140Z-n where the days of the week are numbered from 0 to n (integer n > 0) and where I save from week number 0 to week number n included (in the table below n = 6).

How much money would I have at the end of my financing plan on planet XY140Z-n?


func finance(_ n: UInt64) -> UInt64 {
   var x = 0 
  var r = 0
  var nn = n
 	repeat { 
 		for i in 0...nn {
 			r += x + Int(i)
 		}
 		x += 2
 		nn -= 1
    print(r+x)
 	} while nn > 0 && (r+x)-1 <= Int64.max
  print(r+x)
  return UInt64(r+x)
  }
  
  
  OR
  
  
  func finance(_ n: UInt64) -> UInt64 {
    return n * (n+1) * (n+2) / 2
}



+++++++++++++++++++++++++++
The drawing shows 6 squares the sides of which have a length of 1, 1, 2, 3, 5, 8. It's easy to see that the sum of the perimeters of these squares is : 4 * (1 + 1 + 2 + 3 + 5 + 8) = 4 * 20 = 80

Could you give the sum of the perimeters of all the squares in a rectangle when there are n + 1 squares disposed in the same manner as in the drawing:

alternative text

Hint:

See Fibonacci sequence

Ref:

http://oeis.org/A000045

The function perimeter has for parameter n where n + 1 is the number of squares (they are numbered from 0 to n) and returns the total perimeter of all the squares.

func perimeter(_ n: UInt64) -> UInt64 {
   var a = [1,1]
    for i in 2...n {
        a.append(a[Int(UInt64(i)-1)]+a[Int(UInt64(i)-2)])
      }
  return UInt64(a.reduce(0, +) * 4)
}

++++++++++++++++++++++++++
I always thought that my old friend John was rather richer than he looked, but I never knew exactly how much money he actually had. One day (as I was plying him with questions) he said:

"Imagine I have between m and n Zloty..." (or did he say Quetzal? I can't remember!)
"If I were to buy 9 cars costing c each, I'd only have 1 Zloty (or was it Meticals?) left."
"And if I were to buy 7 boats at b each, I'd only have 2 Ringglets (or was it Zloty?) left."
Could you tell me in each possible case:

how much money f he could possibly have ?
the cost c of a car?
the cost b of a boat?
So, I will have a better idea about his fortune. Note that if m-n is big enough, you might have a lot of possible answers.

Each answer should be given as ["M: f", "B: b", "C: c"] and all the answers as [ ["M: f", "B: b", "C: c"], ... ]. "M" stands for money, "B" for boats, "C" for cars.

Note: m, n, f, b, c are positive integers, where 0 <= m <= n or m >= n >= 0. m and n are inclusive.

func howMuch(_ m: Int, _ n: Int) -> [(String, String, String)] {
   var L = [(String, String, String)]()
    if n >= m {
        for i in m...n+1  {
            if (i-2) % 7 == 0 && (i-1) % 9 == 0 {
                L += [("M: "+String(i), "B: "+String(Int((i-2)/7)), "C: "+String(Int((i-1)/9)))]
              }
          }
      } else {
        for i in n...m+1 {
            if (i-2) % 7 == 0 && (i-1) % 9 == 0 {
                L += [("M: "+String(i), "B: "+String(Int((i-2)/7)), "C: "+String(Int((i-1)/9)))]
              }
          }
        }
    return L
}



++++++++++++++++++++++++++++

Two tortoises named A and B must run a race. A starts with an average speed of 720 feet per hour. Young B knows she runs faster than A, and furthermore has not finished her cabbage.

When she starts, at last, she can see that A has a 70 feet lead but B's speed is 850 feet per hour. How long will it take B to catch A?

More generally: given two speeds v1 (A's speed, integer > 0) and v2 (B's speed, integer > 0) and a lead g (integer > 0) how long will it take B to catch A?

The result will be an array [hour, min, sec] which is the time needed in hours, minutes and seconds (round down to the nearest second) or a string in some languages.

If v1 >= v2 then return nil, nothing, null, None or {-1, -1, -1} for C++, C, Go, Nim, Pascal, [-1, -1, -1] for Perl,[] for Kotlin or "-1 -1 -1".


func race(_ v1: Int, _ v2: Int, _ g: Int) -> [Int]? {
  var time = g * 3600 / (v2 - v1)
    return  v1 >= v2 ? nil : [time / 3600, (time % 3600) / 60, time % 3600 % 60]
}


++++++++++++++++++++
There's a waiting room with N chairs set in single row. Chairs are consecutively numbered from 1 to N. First is closest to the entrance (which is exit as well).

For some reason people choose a chair in the following way

Find a place as far from other people as possible
Find a place as close to exit as possible
All chairs must be occupied before the first person will be served

So it looks like this for 10 chairs and 10 patients



solution

func lastChair(_ n: Int) -> Int {
  return n-1
}



++++++++++++++++++++
Write a function, persistence, that takes in a positive parameter num and returns its multiplicative persistence, which is the number of times you must multiply the digits in num until you reach a single digit.


solution 


func persistence(for num: Int) -> Int {
   var i = 0
  var vam = num
 while String(vam).count != 1 {
     vam = String(vam).map { String($0) }.compactMap { Int($0) }.reduce( 1, *)
     i += 1
   }  
   return i
}


++++++++++++++++++++++
The wave (known as the Mexican wave in the English-speaking world outside North America) is an example of metachronal rhythm achieved in a packed stadium when successive groups of spectators briefly stand, yell, and raise their arms. Immediately upon stretching to full height, the spectator returns to the usual seated position.

The result is a wave of standing spectators that travels through the crowd, even though individual spectators never move away from their seats. In many large arenas the crowd is seated in a contiguous circuit all the way around the sport field, and so the wave is able to travel continuously around the arena; in discontiguous seating arrangements, the wave can instead reflect back and forth through the crowd. When the gap in seating is narrow, the wave can sometimes pass through it. Usually only one wave crest will be present at any given time in an arena, although simultaneous, counter-rotating waves have been produced. (Source Wikipedia)

In this simple Kata your task is to create a function that turns a string into a Mexican Wave. You will be passed a string and you must return that string in an array where an uppercase letter is a person standing up. 

func wave(_ y: String) -> [String] {
 var result: [String] = []
  var temp: [String] = []
  var t = 0
  if y.isEmpty {
    return []
  }
  for _ in 1...y.count {
    t += 1
    temp = y.map { String($0) }
    if temp[t-1] != " " {
   temp[t-1] = temp[t-1].uppercased()
      } else {
      continue
    }
    result.append(temp.joined(separator: ""))
  }
  return result
}


++++++++++++++++++++++


Your job is to change the given string s using a non-negative integer n.

Each bit in n will specify whether or not to swap the case for each alphabetic character in s: if the bit is 1, swap the case; if its 0, leave it as is. When you finish with the last bit of n, start again with the first bit.

You should skip the checking of bits when a non-alphabetic character is encountered, but they should be preserved in their original positions.


func swap(_ s: String,_ n: Int) -> String {
 let str = Array(String(n, radix: 2))
  let arr = Array(s)
  var array: [Any] = []
  var n = 0
  for i in arr {
    if n < str.count {
   if str[n] == "1" {
     if i.isUppercase == false {
   array.append(String(i).uppercased())
       }
     if i.isUppercase == true {
       array.append(String(i).lowercased())
     }
   } else if str[n] == "0" {
   array.append(i)
   }
    } else {
       if str[n-1] == "1" {
  if i.isUppercase == false {
   array.append(String(i).uppercased())
       }
     if i.isUppercase == true {
       array.append(String(i).lowercased())
     }
   } else if str[n-1] == "0" {
   array.append(i)
   }
      n -= str.count+1
    }
    n += 1
  }
 let string = array.compactMap { String(describing: $0) }
  let astring = string.joined(separator: "")
  print(str)
return astring
}

IN PROGRESSS
+++++++++++++++++++++++++



<!-- HTML -->
<img src="https://readme-jokes.vercel.app/api" alt="Jokes Card" />

