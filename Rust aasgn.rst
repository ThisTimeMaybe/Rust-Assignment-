1. Implement a function that checks whether a given string is a
   palindrome or not.

fn is_palindrome(s: &str) -> bool { let mut chars = s.chars(); let mut
left = 0; let mut right = s.len() - 1;

::

   while left < right {
       if chars.nth(left) != chars.nth_back(right) {
           return false;
       }
       left += 1;
       right -= 1;
   }
   true

}

fn main() { let input = “level”; if is_palindrome(input) { println!(“{}
is a palindrome.”, input); } else { println!(“{} is not a palindrome.”,
input); } }

2. Given a sorted array of integers, implement a function that returns
   the index of the first occurrence of a given number.

fn first_occurrence(arr: &[i32], target: i32) -> Option { let mut low =
0; let mut high = arr.len() - 1; let mut result = None;

::

   while low <= high {
       let mid = low + (high - low) / 2;

       if arr[mid] == target {
           result = Some(mid);
           high = mid - 1; // Continue searching on the left side
       } else if arr[mid] < target {
           low = mid + 1;
       } else {
           high = mid - 1;
       }
   }

   result

}

fn main() { let sorted_arr = vec[1, 2, 2, 3, 4, 5, 5, 5, 6, 7, 8, 9];
let target = 5; match first_occurrence(&sorted_arr, target) {
Some(index) => println!(“The first occurrence of {} is at index {}”,
target, index), None => println!(“{} is not found in the array.”,
target), } }

3. Given a string of words, implement a function that returns the
   shortest word in the string.

fn shortest_word(s: &str) -> Option<&str> { s.split_whitespace()
.min_by_key(|word\| word.len()) }

fn main() { let input = “The quick brown fox jumps over the lazy dog”;
match shortest_word(input) { Some(shortest) => println!(“The shortest
word is: {}”, shortest), None => println!(“No words found in the
string.”), } }

4. Implement a function that checks whether a given number is prime or
   not.

fn is_prime(n: u64) -> bool { if n <= 1 { return false; }

::

   let mut i = 2;
   while i * i <= n {
       if n % i == 0 {
           return false;
       }
       i += 1;
   }
   true

}

fn main() { let number = 29; if is_prime(number) { println!(“{} is a
prime number.”, number); } else { println!(“{} is not a prime number.”,
number); } }

5. Given a sorted array of integers, implement a function that returns
   the median of the array.

fn find_median(arr: &[i32]) -> f64 { let len = arr.len(); if len % 2 ==
0 { // If the number of elements is even let mid_right = len / 2; let
mid_left = mid_right - 1; (arr[mid_left] + arr[mid_right]) as f64 / 2.0
} else { // If the number of elements is odd arr[len / 2] as f64 } }

fn main() { let arr = [1, 2, 3, 4, 5]; let median = find_median(&arr);
println!(“Median: {}”, median);

::

   let arr2 = [1, 2, 3, 4];
   let median2 = find_median(&arr2);
   println!("Median: {}", median2);

}

6. Implement a function that finds the longest common prefix of a given
   set of strings.

fn longest_common_prefix(strings: &[&str]) -> String { if
strings.is_empty() { return String::new(); }

::

   let mut result = String::new();
   let first_string = strings[0];
   let mut char_iterators: Vec<_> = strings.iter().map(|s| s.chars()).collect();

   'outer: loop {
       let mut current_char: Option<char> = None;

       for char_iter in &mut char_iterators {
           match char_iter.next() {
               Some(c) => {
                   if let Some(prev) = current_char {
                       if c != prev {
                           break 'outer;
                       }
                   } else {
                       current_char = Some(c);
                   }
               }
               None => break 'outer,
           }
       }

       if let Some(c) = current_char {
           result.push(c);
       } else {
           break 'outer;
       }
   }

   result

}

fn main() { let strings = [“flower”, “flow”, “flight”]; let prefix =
longest_common_prefix(&strings); println!(“Longest Common Prefix: {}”,
prefix);

::

   let strings2 = ["dog", "racecar", "car"];
   let prefix2 = longest_common_prefix(&strings2);
   println!("Longest Common Prefix: {}", prefix2);

}

7. Implement a function that returns the kth smallest element in a given
   array.

fn kth_smallest(arr: &[i32], k: usize) -> Option { if k == 0 \|\| k >
arr.len() { return None; }

::

   let mut sorted_arr = arr.to_vec();
   sorted_arr.sort();

   Some(sorted_arr[k - 1])

}

fn main() { let arr = [7, 10, 4, 3, 20, 15]; let k = 3; match
kth_smallest(&arr, k) { Some(result) => println!(“The {}th smallest
element is: {}”, k, result), None => println!(“Invalid input. Unable to
find the {}th smallest element.”, k), } }

8. Given a binary tree, implement a function that returns the maximum
   depth of the tree.

// Definition for a binary tree node. #[derive(Debug, PartialEq, Eq)]
pub struct TreeNode { pub val: i32, pub left: Option<Rc<RefCell>>, pub
right: Option<Rc<RefCell>>, }

use std::rc::Rc; use std::cell::RefCell;

impl TreeNode { #[allow(dead_code)] pub fn new(val: i32) -> Self {
TreeNode { val, left: None, right: None, } } }

fn max_depth(root: Option<Rc<RefCell>>) -> i32 { match root { Some(node)
=> { let node = node.borrow(); let left_depth =
max_depth(node.left.clone()); let right_depth =
max_depth(node.right.clone()); 1 + left_depth.max(right_depth) } None =>
0, } }

| fn main() { // Example tree: // 3 // /
| // 9 20 // /
| // 15 7 let root = Some(Rc::new(RefCell::new(TreeNode { val: 3, left:
  Some(Rc::new(RefCell::new(TreeNode::new(9)))), right:
  Some(Rc::new(RefCell::new(TreeNode { val: 20, left:
  Some(Rc::new(RefCell::new(TreeNode::new(15)))), right:
  Some(Rc::new(RefCell::new(TreeNode::new(7)))), }))), })));

::

   let depth = max_depth(root);
   println!("Maximum depth of the binary tree: {}", depth);

}

9. Reverse a string in Rust

fn reverse_string(s: &mut String) { let len = s.len(); let mut left = 0;
let mut right = len - 1;

::

   while left < right {
       s.as_mut_bytes().swap(left, right);
       left += 1;
       right -= 1;
   }

}

fn main() { let mut s = String::from(“hello”); println!(“Original
string: {}”, s);

::

   reverse_string(&mut s);

   println!("Reversed string: {}", s);

}

10. Check if a number is prime in Rust

fn is_prime(n: u64) -> bool { if n <= 1 { return false; }

::

   let mut i = 2;
   while i * i <= n {
       if n % i == 0 {
           return false;
       }
       i += 1;
   }
   true

}

fn main() { let number = 29; if is_prime(number) { println!(“{} is a
prime number.”, number); } else { println!(“{} is not a prime number.”,
number); } }

11. Merge two sorted arrays in Rust

fn merge_sorted_arrays(arr1: &[i32], arr2: &[i32]) -> Vec { let mut
result = Vec::with_capacity(arr1.len() + arr2.len()); let (mut i, mut j)
= (0, 0);

::

   while i < arr1.len() && j < arr2.len() {
       if arr1[i] < arr2[j] {
           result.push(arr1[i]);
           i += 1;
       } else {
           result.push(arr2[j]);
           j += 1;
       }
   }

   // Add remaining elements from arr1
   while i < arr1.len() {
       result.push(arr1[i]);
       i += 1;
   }

   // Add remaining elements from arr2
   while j < arr2.len() {
       result.push(arr2[j]);
       j += 1;
   }

   result

}

fn main() { let arr1 = [1, 3, 5, 7, 9]; let arr2 = [2, 4, 6, 8, 10];

::

   let merged_array = merge_sorted_arrays(&arr1, &arr2);

   println!("Merged sorted array: {:?}", merged_array);

}

12. Find the maximum subarray sum in Rust

fn max_subarray_sum(arr: &[i32]) -> i32 { if arr.is_empty() { return 0;
}

::

   let mut max_ending_here = arr[0];
   let mut max_so_far = arr[0];

   for &num in arr.iter().skip(1) {
       max_ending_here = max_ending_here.max(0) + num;
       max_so_far = max_so_far.max(max_ending_here);
   }

   max_so_far

}

fn main() { let arr = [-2, 1, -3, 4, -1, 2, 1, -5, 4]; let max_sum =
max_subarray_sum(&arr); println!(“Maximum subarray sum: {}”, max_sum); }
