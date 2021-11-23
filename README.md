


SWIFT version

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

