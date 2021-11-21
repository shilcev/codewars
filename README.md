


SWIFT version




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
    print(y)
    return []
  }
  for _ in 1...y.count {
    t += 1
    temp = y.map { String($0) }
    temp[t-1] = temp[t-1].uppercased()
    result.append(temp.joined(separator: ""))
  }
  print(result)
  return result
}



in process
++++++++++++++++++++++



<!-- HTML -->
<img src="https://readme-jokes.vercel.app/api" alt="Jokes Card" />

