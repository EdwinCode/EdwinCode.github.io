# EdwinCode.github.io
My site where I toss some ideas.

Currently working on learning Go. I may write done some notes here.
I will aslo be attempting LeetCode problems.

# April 3, 2021
I decided to tackle the Reverse Integer problem on LeetCode today so here is my final solution to it:

    class Solution {
        public int reverse(int x) {
    
            boolean isNegative = (x < 0) ? true : false;
            x = Math.abs(x);
            int powersOfTen = -1;
            for (int i = x; i > 0; i /= 10) {
                powersOfTen++;
            }

            int trueResult = 0;
            long result = 0;
            for (int i = x; i > 0; i /= 10) {
                result += Math.pow(10, powersOfTen) * (i % 10);
                trueResult += Math.pow(10, powersOfTen) * (i % 10);
                powersOfTen--;
            }

            if (result > Integer.MAX_VALUE) {
                return 0;
            }
            if (isNegative) {
                if (-1 * result < Integer.MIN_VALUE) {
                    return 0;
                }
                return -1 * trueResult;
            }
            return trueResult;
        }
    }

This was just as fast as the solution they have posted and uses about the same amount memory (a little less actually) according to their tests. Although, I did enjoy reading on why they went with their solution since it uses knowledge on when an integer will overflow and as such does not need to use a long to determine if the integer is outside its allowed range.

# March 31, 2021

Here is my final solution to the Add Two Numbers problem:

    class Solution {
  
      public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
          // Allows us to avoid fenceposting
          ListNode dummyHead = new ListNode(0);
          // Copy the lists so that we do not lose the originals
          ListNode current1 = l1;
          ListNode current2 = l2;
          ListNode nextNode = dummyHead;
          // Will hold the carry-over value between addition of two nodes
          int carry = 0;

          // once both lists have ended we exit
          while (current1 != null || current2 != null) {
              // if one node is null then add the other node to 0
              int val1 = current1 != null ? current1.val : 0;
              int val2 = current2 != null ? current2.val : 0;
              int sum = (val1 + val2 + carry);
              int addVal = sum % 10;
              carry = sum / 10;
              nextNode.next = new ListNode(addVal);

              // if either node is currently null do not move it forward
              if (current1 != null) {
                  current1 = current1.next;
              }
              if (current2 != null) {
                  current2 = current2.next;
              }
              // move the node we are constructing forward
              nextNode = nextNode.next;
          }
          // if carry-over value is 1 add it as the final node
          if (carry != 0) {
              nextNode.next = new ListNode(carry);
          }
          // return the true first value
          return dummyHead.next;
      }
    }

Initially I had a fencepost solution which was slightly slower than the solution above, however, after some research I found out that you could use a fake beginning node to avoid the fencepost route. What really helped me was understanding the implementation of a LinkedList which I learned by reading Chapter 16 of Building Java Programs 5e. With that knowledge, I ignored my previous attempt at the problem and started fresh.

# March 30, 2021

Read up on the implementation of a LinkedList via Building Java Programs 5e and have gained a lot of insight on how to approach the Add Two Numbers problem from LeetCode in a simpler manner.

# March 29, 2021

Did a first attempt at the Add Two Numbers problem which utilizes information about the implementation of a LinkedList. Ran into a problem where my nodes are in the wrong spot by one location. As such, I will read up on LinkedList implementation to attempt this problem again with a more solid understanding.
