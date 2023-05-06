Download Link: https://assignmentchef.com/product/solved-ece421-assignment-7-concurrency
<br>
<strong>Question 1:</strong> Consider the following code:

<table width="630">

 <tbody>

  <tr>

   <td width="630">#[derive(Clone,Debug)] struct Bank{  accounts:Arc&lt;Mutex&lt;Vec&lt;i32&gt;&gt;&gt;}  impl Bank{   fn new(n:usize)-&gt;Self{          let mut v = Vec::with_capacity(n);     for _ in 0..n{v.push(0);}Bank{                accounts:Arc::new(Mutex::new(v)),}}    fn transfer(&amp;self, from:usize, to:usize, amount:i32)-&gt;Result&lt;(),()&gt;{…..}}</td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Create a <em>transfer</em> function for type “Bank” with the following signature:</li>

</ul>

<em>pub fn transfer(&amp;self, from:usize, to:usize, amount:i32)-&gt;Result&lt;(),()&gt; </em>

The function returns an error if either account [from, to] does not exist. Assuming both accounts exist, the function should transfer the amount and print as follows:

<em>Amount of $33 transferred from account id: 16 to account id: 15. </em>

<ul>

 <li>In the main function, you should simulate at least 10 users and make each running on their own thread, going into the bank, making a payment to somebody else’s account. Utilize the following structure modeling a person in your solution:</li>

</ul>

<table width="630">

 <tbody>

  <tr>

   <td width="630">struct Person{  ac_id:usize,  buddy_id:usize,} impl Person{pub fn new(id:usize,b_id:usize)-&gt;Self{Person{ac_id:id,           buddy_id:b_id}}}</td>

  </tr>

 </tbody>

</table>

<strong>Question 2:</strong> Consider the following code:

<table width="639">

 <tbody>

  <tr>

   <td width="639">use std::thread;  use std::time::Duration;   fn main(){      let mut sample_data = vec![1, 81, 107];       for i in 0..10{          thread::spawn(move || { sample_data[0] += i; }); // fails here}        thread::sleep(Duration::from_millis(50));}</td>

  </tr>

 </tbody>

</table>

a- The previous code will not run, explain why (Hint: think about ownership). b- Apply Mutex to the previous code, so it runs.

<strong>Upload your answer as a Rust Project with the name “Assignment7_Q2” Question 3:</strong> Consider the following code:

<table width="639">

 <tbody>

  <tr>

   <td width="639">use rayon::prelude::*;fn main() {     let quote = “Some are born great, some achieve greatness, and some have greatness thrust upon them.”.to_string();find_words(quote,’s’);}    fn find_words(quote:String, ch:char){ let words: Vec&lt;_&gt; = quote.split_whitespace().collect();         <strong>// add your code here: </strong>let words_with_a: Vec&lt;_&gt; = <strong>………</strong>       println!(“The following words contain the letter {:?}: {:?}”, ch, words_with_ch);}</td>

  </tr>

 </tbody>

</table>

Utilize the rayon crate to iterate through words parallelly and print the words that contain a specific character <em>ch</em>.

<strong>Upload your answer as a Rust Project with the name “Assignment7_Q3”. </strong>

<strong>   </strong>

<strong>  </strong>

<strong>Question 4:</strong> Consider the following code:

use rayon::prelude::*;




fn concurrent_quick_sort&lt;T&gt;(v: &amp;mut [T]) {

<strong>    //add your code here: </strong>

<strong>    //uses partition fn, multiple options exist. </strong>

<strong>    //use rayon for concurrency. </strong>

}

fn partition&lt;T&gt;(v: &amp;mut [T]) -&gt; usize {

<strong>    //add your code here: </strong>

}

In Concurrent quick sort, each part is processed by an independent thread (i.e., different threads will find the pivot element in each part recursively). Check following diagram. Here PE stands for Pivot Element.

Array ———————————————————————————- Thread 0

Array —————————————–PE0———————————–

Thread 1                            Thread 2

Array ——————-PE1—————-PE0————–PE2—————–

Thread 3           Thread 4           Thread 5           Thread 6

If you need more information, you can check out this video: <a href="https://www.youtube.com/watch?v=kbkpILBv6fM">https://www.youtube.com/watch?v=kbkpILBv6fM</a>

The partitioning step is accomplished through the use of a <em>parallel prefix sum</em> algorithm

(https://en.wikipedia.org/wiki/Prefix_sum) to compute an index for each array element in its section of the partitioned array.