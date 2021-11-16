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
   let i = 0
  var vam = [""]
  // while String(num).count != 1 {
     vam = String(num).components(separatedBy: [""])//.reduce((a,b)=>a*b);
   //  i += 1
 //  }
 //  return i
  
  
  return 0 
}



IN PROGRESSS

++++++++++++++++++++++
