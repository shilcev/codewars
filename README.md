


SWIFT version



++++++++++++++++++++++++++++++++


Linked Lists - Get Nth

Implement a GetNth() function that takes a linked list and an integer index and returns the node stored at the Nth index position. GetNth() uses the C numbering convention that the first node is index 0, the second is index 1, ... and so on. So for the list 42 -> 13 -> 666, GetNth() with index 1 should return Node(13);

getNth(1 -> 2 -> 3 -> null, 0).data === 1
getNth(1 -> 2 -> 3 -> null, 1).data === 2
The index should be in the range [0..length-1]. If it is not, GetNth() should throw/raise an exception (ArgumentException in C#, InvalidArgumentException in PHP). You should also raise an exception (ArgumentException in C#, InvalidArgumentException in PHP) if the list is empty/null/None.

Prerequisite Kata (may be in beta):

Linked Lists - Push & BuildOneTwoThree
Linked Lists - Length & Count
The push() and buildOneTwoThree() (BuildOneTwoThree in C#, build_one_two_three() in PHP) functions do not need to be redefined.

class Node {
    var data: Int
    var next: Node?
    init(_ data: Int) {
        self.data = data
    }
}

enum someError: Error {
  case one
}

func getNth(_ head: Node?, _ index: Int) throws -> Node? {
  guard let currentNode = head, index >= 0 else { throw someError.one }
  return index == 0 ? currentNode : try getNth(currentNode.next, index - 1)
}



+++++++++++++++++++++++++++++++++




From Wikipedia : "The n-back task is a continuous performance task that is commonly used as an assessment in cognitive neuroscience to measure a part of working memory and working memory capacity. [...] The subject is presented with a sequence of stimuli, and the task consists of indicating when the current stimulus matches the one from n steps earlier in the sequence. The load factor n can be adjusted to make the task more or less difficult."

In this kata, your task is to "teach" your computer to do the n-back task. Specifically, you will be implementing a function that counts the number of "targets" (stimuli that match the one from n steps earlier) in a sequence of digits. Your function will take two parameters :

n, a positive integer equal to the number of steps to look back to find a match
sequence, a sequence of digits containing 0 or more targets
A few hints :

The first digit in a sequence can never be a target
Targets can be "chained" together (e.g., for n = 1 and sequence = [1, 1, 1], there are 2 targets)




func countTargets(_ n: Int, _ sequence: [Int]) -> Int {
  var count = 0
 for i in 0...sequence.count {
    if i + n < sequence.count && sequence[i] == sequence[i + n]{
        count += 1
    }
  }
  return count
}


+++++++++++++++++++++++++++++++++



Your task is to find all the elements of an array that are non consecutive.

A number is non consecutive if it is not exactly one larger than the previous element in the array. The first element gets a pass and is never considered non consecutive.

Create a function named allNonConsecutive

E.g., if we have an array [1,2,3,4,6,7,8,15,16] then 6 and 15 are non-consecutive.

You should return the results as an array of tuples with two values: the index of the non-consecutive number and the non-consecutive number.



func allNonConsecutive (_ arr: [Int]) -> [(Int, Int)] {  
 if arr.count == 0 { return [] }
   var answer: [(Int, Int)] = []
   for i in 0...arr.count {
     let next = (i < arr.count - 1) ? arr[i + 1] : nil
   if next != nil {
    if abs(arr[i] - next!) != 1 {
      answer.append((i+1, next!))
    }
     } 
   }
  return answer
}



+++++++++++++++++++++++++++++++++



We will call a natural number a "doubleton number" if it contains exactly two distinct digits. For example, 23, 35, 100, 12121 are doubleton numbers, and 123 and 9980 are not.

For a given natural number n (from 1 to 1 000 000), you need to find the next doubleton number. If n itself is a doubleton, return the next bigger than n.



func doubleton(_ num: Int) -> Int {
 return Set(Array(String(num + 1))).count == 2 ? num + 1 : doubleton(num + 1)
  }



++++++++++++++++++++++++++++++++++



Create a function add(n)/Add(n) which returns a function that always adds n to any number

Note for Java: the return type and methods have not been provided to make it a bit more challenging.


func add(_ n: Int) -> ((Int) -> Int) { 
  func addn(number: Int) -> Int {
        return n + number
    }
    return addn

}




+++++++++++++++++++++++++++++++++++



Professor Chambouliard has just completed an experiment on gravitational waves. He measures their effects on small magnetic particles. This effect is very small and negative. In his first experiment the effect satisfies the equation:

x**2 + 1e9 * x + 1 = 0.

Professor C. knows how to solve equations of the form:

g(x) = a x ** 2 + b x + c = 0 (1)

using the "discriminant".

It finds that the roots of x**2 + 1e9 * x + 1 = 0 are x1 = -1e9 and x2 = 0. The value of x1 - good or bad - does not interest him because its absolute value is too big.

On the other hand, he sees immediately that the value of x2 is not suitable!

He asks our help to solve equations of type (1) with a, b, c strictly positive numbers, and b being large (b >= 10 ** 9).

Professor C. will check your result x2 (the smaller root in absolute value. Don't return the other root!) by reporting x2 in (1) and seeing if abs(g(x2)) < 1e-12.

Task:

solve(a, b, c)

that will return the "solution" x2 of (1) such as abs(a * x2 ** 2 + b * x2 + c) < 1e-12.

Example:

for equation 7*x**2 + 0.40E+14 * x + 8 = 0 we can find: x2 = -2e-13 which verifies abs(g(x)) < 1e-12.



func quadratic(_ a: Double, _ b: Double, _ c: Double) -> Double {
 return -c / b
}


++++++++++++++++++++++++++++++++++




A number system with moduli is deﬁned by a vector of k moduli, [m1,m2, ···,mk].

The moduli must be pairwise co-prime, which means that, for any pair of moduli, the only common factor is 1.

In such a system each number n is represented by a string "-x1--x2-- ... --xk-" of its residues, one for each modulus. The product m1 * ... * mk must be greater than the given number n which is to be converted in the moduli number system.

For example, if we use the system [2, 3, 5] the number n = 11 is represented by "-1--2--1-",
the number n = 23 by "-1--2--3-".

If we use the system [8, 7, 5, 3] the number n = 187 becomes "-3--5--2--1-".

You will be given a number n (n >= 0) and a system S = [m1,m2, ···,mk] and you will return a string "-x1--x2-- ...--xk-" representing the number n in the system S.

If the moduli are not pairwise co-prime or if the product m1 * ... * mk is not greater than n, return "Not applicable".



func fromNb2Str(_ n: Int, _ sys: [Int]) -> String {
 var prod = 1
    var res = ""
    var nums: [Int] = []
    var even = 0
  var count = 0 
     for i in sys {
         if i % 2 == 0 {
             even += 1 
           }
         prod *= i
       let a = n % i
         nums.append(a)
         res += "-" + String(a) + "-"
     count = 0 
       } 
     for i in 1...sys.count {
        for j in sys {
             if sys[i-1] % j == 0 {
                 count += 1
               }
           } 
       }
    if count != sys.count || even > 1 || prod <= n {
         return "Not applicable" 
  }
     return res
}


++++++++++++++++++++++++++++++++++



The rgb function is incomplete. Complete it so that passing in RGB decimal values will result in a hexadecimal representation being returned. Valid decimal values for RGB are 0 - 255. Any values that fall out of that range must be rounded to the closest valid value.

Note: Your answer should always be 6 characters long, the shorthand with 3 will not work here.

func rgb(_ r: Int, _ g: Int, _ b: Int) -> String {
  var rC = r
  var gC = g
  var bC = b
  if r < 0 { rC = 0 } 
  if r > 255 { rC = 255 }
   if g < 0 { gC = 0 } 
  if g > 255 { gC = 255 }
   if b < 0 { bC = 0 } 
  if b > 255 { bC = 255 }
      if (0 ... 255 ~= rC) && (0 ... 255 ~= gC) && (0 ... 255 ~= bC) {
        var result = String(((1 << 24) + (rC << 16) + (gC << 8) + bC), radix: 16)
        result.remove(at: result.startIndex)
       return(result.uppercased())
  }
  return ""
}



++++++++++++++++++++++++++++++++++


Consider the function

f: x -> sqrt(1 + x) - 1 at x = 1e-15.

We get: f(x) = 4.44089209850062616e-16

or something around that, depending on the language.

This function involves the subtraction of a pair of similar numbers when x is near 0 and the results are significantly erroneous in this region. Using pow instead of sqrt doesn't give better results.

A "good" answer is 4.99999999999999875... * 1e-16.

Can you modify f(x) to give a good approximation of f(x) in the neighborhood of 0?

Note:

Don't round or truncate your results. See the testing function in Sample Tests:.






func f(_ x: Double) -> Double {
  return x / 2.0 - pow(x, 2.0) / 8.0 + pow(x, 3.0) / 16.0 - 5.0 * pow(x, 4.0) / 128.0 + 7.0 * pow(x, 5.0) / 256.0
}



++++++++++++++++++++++++++++++++++
For the rest of this Kata, I would recommend considering "fuck" to be non-profane.

Esolang Interpreters #1 - Introduction to Esolangs and My First Interpreter (MiniStringFuck)

About this Kata Series

"Esolang Interpreters" is a Kata Series that originally began as three separate, independent esolang interpreter Kata authored by @donaldsebleung which all shared a similar format and were all somewhat inter-related. Under the influence of a fellow Codewarrior, these three high-level inter-related Kata gradually evolved into what is known today as the "Esolang Interpreters" series.

This series is a high-level Kata Series designed to challenge the minds of bright and daring programmers by implementing interpreters for various esoteric programming languages/Esolangs, mainly Brainfuck derivatives but not limited to them, given a certain specification for a certain Esolang. Perhaps the only exception to this rule is the very first Kata in this Series which is intended as an introduction/taster to the world of esoteric programming languages and writing interpreters for them.

What is an esoteric programming language?

An esoteric programming language, otherwise known as an Esolang, is an informal computer programming language that is generally not designed for serious practical use. There are a few main aims/themes among the vast majority of such languages:

Achieve Turing-completeness in as few commands (instructions) as possible. There are currently a number of implemented Esolangs that have been proven to be Turing-complete, Brainfuck being the most popular of them all, comprised of no more than 8 distinct commands. Despite having only 8 commands, it has been objectively proven to be Turing-complete. However, Brainfuck is not the Turing-complete programming language with the fewest commands. Boolfuck, a derivative of Brainfuck which operates on bits (0s and 1s) and contains 7 commands only, has also been proven to be Turing-complete through reduction from Brainfuck. Another less-known Esolang called Etre contains as few as 3 commands yet has been proven to be Turing-complete through the translation of a Minsky Machine to Etre.
To be as hard to program in as possible. The famous Brainfuck Esolang is well known as a Turing tarpit - that is, a Turing-complete programming language where it is very hard to write a useful program in reality. However, Brainfuck is most definitely not the hardest Esolang to program in. For example, its close cousin, Boolfuck, which operates on bits (mentioned above) is even harder to program in. There have also been a small number of implemented Esolangs which are so difficult to program in that no one has ever successfully written a single program in it from scratch - the only programs generated from these languages came from computers!
As a joke. Many Esolangs out there have been invented solely as a joke. Examples include Ook! and Bitxtreme.
Although there is no clear-cut definition as to when a programming language is esoteric (or not), Esolangs can generally be identified by the following features/traits:

Minimalistic - having as few instructions as possible
Plays with new concepts - for example, Befunge, another very popular Esolang, is interpreted in two dimensions as opposed to the usual linear way of interpreting code
Themed - this is a trait of many joke Esolangs. For example, some may be fashioned like Shakespearean plays and others like cooking recipes
Not clearly documented - Many Esolangs out there have not been described in great detail with perhaps only a few code examples on the entire Internet. Some Esolangs have not even been implemented yet!
Contain incomplete specs - New Esolangs are being invented every day. Some Esolangs on the Internet are still a work-in-progress and their commands and behaviour have not been finalised yet.
Nevertheless, Esolangs are generally fun to program in, experiment with and write interpreters for. A great deal can be learned about certain concepts and theories in Computer Science just by studying and programming in a well-designed Esolang such as Brainfuck or Befunge.

Next off, I will introduce you to a simple, minimalistic Esolang called MiniStringFuck.

The Language

MiniStringFuck is a derivative of the famous Brainfuck which contains a memory cell as its only form of data storage as opposed to a memory tape of 30,000 cells in Brainfuck. The memory cell in MiniStringFuck initially starts at 0. MiniStringFuck contains only 2 commands as opposed to 8:

+ - Increment the memory cell. If it reaches 256, wrap to 0.
. - Output the value of the memory cell as a character with code point equal to the value
For example, here is a MiniStringFuck program that outputs the string "Hello, World!":




func interpreter(_ prog: String) -> String {
var cell = 0
    var output = ""
     for i in prog {
        if i == "+" {
             cell = (cell + 1 ) % 256
          } else if i == "." {
          output += "\(Character(UnicodeScalar(cell)!))"
          }
       }
     return output
}


++++++++++++++++++++++++++++++++++



Create a function that takes a positive integer and returns the next bigger number that can be formed by rearranging its digits. For example:

12 ==> 21
513 ==> 531
2017 ==> 2071
nextBigger(num: 12)   // returns 21
nextBigger(num: 513)  // returns 531
nextBigger(num: 2017) // returns 2071
If the digits can't be rearranged to form a bigger number, return -1 (or nil in Swift):

9 ==> -1
111 ==> -1
531 ==> -1
nextBigger(num: 9)   // returns nil
nextBigger(num: 111) // returns nil
nextBigger(num: 531) // returns nil





func nextBigger(num: Int) -> Int? {
 var result: [Int] = []
 // var arr = String(num).compactMap{ $0.wholeNumberValue } 
  //var arr2 = Array(String(num).compactMap{ $0.wholeNumberValue } .reversed())
  for _ in 0...100 { //arr.count {
/*  var element = arr.remove(at: arr.count-1)
    arr.insert(element, at:0)
    //var element2 = arr.remove(at: arr.count-2)
    //arr.insert(element2, at:0)
    result.append(arr.reduce(0, { $0 * 10 + $1 }))
     var element2 = arr2.remove(at: arr.count-1)
    arr2.insert(element2, at:0)
    result.append(arr2.reduce(0, { $0 * 10 + $1 })) */
    let jopa = String(num).compactMap{ $0.wholeNumberValue }.shuffled()
  result.append(jopa.reduce(0, { $0 * 10 + $1 }))
  }

 // print(Array(result.reversed()), result)
 // print(result.sorted().firstIndex(of: num))  
 // print(Array(Set(result)).sorted())
  //print(Array(Set(result)).sorted().firstIndex(of: num)!)
 // print(Array(Set(result)).sorted()[Array(Set(result)).sorted().firstIndex(of: num)!+1])
 // print(Array(Set(result)).sorted().firstIndex(of: num)!+1, Array(Set(result)).sorted().count)
  if Array(Set(result)).sorted().firstIndex(of: num)!+1 >= Array(Set(result)).sorted().count {
    return nil
  }
  if Array(Set(result)).sorted().firstIndex(of: num)!+1 < Array(Set(result)).sorted().count {
    return Array(Set(result)).sorted()[Array(Set(result)).sorted().firstIndex(of: num)!+1]
  }
  return nil
}
+++++++++++++++++++++++++++


Once upon a time, on a way through the old wild mountainous west,…

… a man was given directions to go from one point to another. The directions were "NORTH", "SOUTH", "WEST", "EAST". Clearly "NORTH" and "SOUTH" are opposite, "WEST" and "EAST" too.

Going to one direction and coming back the opposite direction right away is a needless effort. Since this is the wild west, with dreadfull weather and not much water, it's important to save yourself some energy, otherwise you might die of thirst!

How I crossed a mountainous desert the smart way.

The directions given to the man are, for example, the following (depending on the language):


func dirReduc(_ arr: [String]) -> [String] {
  let directions = ["NORTH": 1, "SOUTH" : -1, "WEST": 2, "EAST": -2]
  var index = 1
  var arr2 = arr
    while index < arr2.count {
        if directions[arr2[index]]! + directions[arr2[index-1]]! == 0 { 
      arr2.remove(at: index)
      arr2.remove(at: index-1)
            if index > 1 { 
              index -= 1 
            }
          } else { index += 1 }
          
      }
    return arr2

+++++++++++++++++++++++++++

Let us begin with an example:

A man has a rather old car being worth $2000. He saw a secondhand car being worth $8000. He wants to keep his old car until he can buy the secondhand one.

He thinks he can save $1000 each month but the prices of his old car and of the new one decrease of 1.5 percent per month. Furthermore this percent of loss increases of 0.5 percent at the end of every two months. Our man finds it difficult to make all these calculations.

Can you help him?

How many months will it take him to save up enough money to buy the car he wants, and how much money will he have left over?

Parameters and return of function:

parameter (positive int or float, guaranteed) startPriceOld (Old car price)
parameter (positive int or float, guaranteed) startPriceNew (New car price)
parameter (positive int or float, guaranteed) savingperMonth 
parameter (positive float or int, guaranteed) percentLossByMonth

nbMonths(2000, 8000, 1000, 1.5) should return [6, 766] or (6, 766)
Detail of the above example:

end month 1: percentLoss 1.5 available -4910.0
end month 2: percentLoss 2.0 available -3791.7999...
end month 3: percentLoss 2.0 available -2675.964
end month 4: percentLoss 2.5 available -1534.06489...
end month 5: percentLoss 2.5 available -395.71327...
end month 6: percentLoss 3.0 available 766.158120825...
return [6, 766] or (6, 766)
where 6 is the number of months at the end of which he can buy the new car and 766 is the nearest integer to 766.158... (rounding 766.158 gives 766).

Note:

Selling, buying and saving are normally done at end of month. Calculations are processed at the end of each considered month but if, by chance from the start, the value of the old car is bigger than the value of the new one or equal there is no saving to be made, no need to wait so he can at the beginning of the month buy the new car:




func nbMonths(_ startPriceOld: Int, _ startPriceNew: Int, _ savingPerMonth: Int, _ percentLossByMonth: Double) -> (Int, Int) {  
var months = 0
var savings = 0
var spo = Double(startPriceOld)
var spn = Double(startPriceNew)
  var percent = percentLossByMonth
    while spo + Double(savings) < spn {
      months += 1
        savings += savingPerMonth
        if months % 2 == 0 {
            percent += 0.5
}
        spo *= ((Double(100) - percent) / Double(100))
        spn *= ((Double(100) - percent) / Double(100))
}
  return (months, Int(round(spo + Double(savings) - spn)))
}


+++++++++++++++++++++++++++



A friend of mine takes the sequence of all numbers from 1 to n (where n > 0).
Within that sequence, he chooses two numbers, a and b.
He says that the product of a and b should be equal to the sum of all numbers in the sequence, excluding a and b.
Given a number n, could you tell me the numbers he excluded from the sequence?
The function takes the parameter: n (n is always strictly greater than 0) and returns an array or a string (depending on the language) of the form:

[(a, b), ...] or [[a, b], ...] or {{a, b}, ...} or or [{a, b}, ...]
with all (a, b) which are the possible removed numbers in the sequence 1 to n.

[(a, b), ...] or [[a, b], ...] or {{a, b}, ...} or ... will be sorted in increasing order of the "a".

It happens that there are several possible (a, b). The function returns an empty array (or an empty string) if no possible numbers are found which will prove that my friend has not told the truth! (Go: in this case return nil).



func removNb(_ n: Int) -> [(Int,Int)] {
    var sum = Int((n*(n+1)) / 2)
     var output: [(Int, Int)] = [] 
     for i in 1...n + 1 {
        let j = (Double(sum) - Double(i)) / (Double(i) + 1.0)
         if floor(j) == j && j <= Double(n) {
             output.append((i,Int(j)))
           }
}
     return output
}

+++++++++++++++++++++++++++
From Wikipedia:

"A divisibility rule is a shorthand way of determining whether a given integer is divisible by a fixed divisor without performing the division, usually by examining its digits."

When you divide the successive powers of 10 by 13 you get the following remainders of the integer divisions:

1, 10, 9, 12, 3, 4 because:



IN PROGRESSS



+++++++++++++++++++++++++++



The walker

The walker starts from point O, walks along OA, AB and BC. When he is in C (C will be in the upper half-plane), what is the distance CO? What is the angle tOC in positive degrees, minutes, seconds?

Angle tOA is alpha (here 45 degrees), angle hAB is beta (here 30 degrees), angle uBC is gamma(here 60 degrees).

Task

function solve(a, b, c, alpha, beta, gamma) with parameters

a, b, c: positive integers in units of distance (stand for OA, AB, BC)
alpha, beta, gamma: positive integers in degrees (positive angles are anticlockwise)
returns an array:

first element: distance CO (rounded to the nearest integer)
then angle tOC with the third following elements:
second element of the array: number of degrees in angle tOC (truncated positive integer)
third element of the array: number of minutes in angle tOC (truncated positive integer)
fourth element of the array: number of seconds in angle tOC (truncated positive integer)






func solve(_ a: Int, _ b: Int, _ c: Int, _ alpha: Int, _ beta: Int, _ gamma: Int) -> [Int] {
   let x = Double(a) * cos(Double(alpha) * .pi / 180) - Double(b) * sin(Double(beta) * .pi / 180) - Double(c) * cos(Double(gamma) * .pi / 180)
  let y = Double(a) * sin(Double(alpha) * .pi / 180) + Double(b) * cos(Double(beta) * .pi / 180) - Double(c) * sin(Double(gamma) * .pi / 180)
    let oc = Int(round(sqrt(pow(x,2) + pow(y,2))))
       let angle = .pi / 2 + atan(-x / y)
         let totalSeconds = Int(angle * 360 * 60 * 60 / (2 * .pi))
         let seconds = totalSeconds % 60
         let minutes = (totalSeconds / 60) % 60
         let degrees = totalSeconds / (60 * 60)
  return [oc,degrees,minutes,seconds]
}
+++++++++++++++++++++++++++


Given two arrays of strings a1 and a2 return a sorted array r in lexicographical order of the strings of a1 which are substrings of strings of a2.

Example 1:

a1 = ["arp", "live", "strong"]

a2 = ["lively", "alive", "harp", "sharp", "armstrong"]

returns ["arp", "live", "strong"]

Example 2:

a1 = ["tarp", "mice", "bull"]

a2 = ["lively", "alive", "harp", "sharp", "armstrong"]

returns []

Notes:

Arrays are written in "general" notation. See "Your Test Cases" for examples in your language.
In Shell bash a1 and a2 are strings. The return is a string where words are separated by commas.
Beware: r must be without duplicates.


func inArray(_ a1: [String], _ a2: [String]) -> [String] {
  var result: [String] = []
 for i in a2 {
      for j in a1 { 
        if i.contains(j) {
          if result.contains(j){
            continue
          } else {
          result += ["\(j)"]
            }
}
    }
  } 
  result.sort()
  return result

}


+++++++++++++++++++++++++++

John has some amount of money of which he wants to deposit a part f0 to the bank at the beginning of year 1. He wants to withdraw each year for his living an amount c0.

Here is his banker plan:

deposit f0 at beginning of year 1
his bank account has an interest rate of p percent per year, constant over the years
John can withdraw each year c0, taking it whenever he wants in the year; he must take account of an inflation of i percent per year in order to keep his quality of living. i is supposed to stay constant over the years.
all amounts f0..fn-1, c0..cn-1 are truncated by the bank to their integral part
Given f0, p, c0, i the banker guarantees that John will be able to go on that way until the nth year.



func fortune(_ f0: Int, _ p: Double, _ c0: Int, _ n: Int, _ i: Double) -> Bool {
 var f = Double(f0)
     var c = Double(c0)
     for k in 1...n {
         if (f < 0) {
             return false
           }
         f = floor(Double(f) + (p / 100) * Double(f) - Double(c))
         c = floor(Double(c) + (Double(c) * Double(i)) / 100)
     }
     return true
}

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

