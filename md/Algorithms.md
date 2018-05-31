## Chapter 1 栈和队列 ##

### 1.1 设计一个有getMin功能的栈 ###

	package chapter1;
	import java.util.*;
	
	public class MyStack1 {
		private Stack<Integer> stackData;
		private Stack<Integer> stackMin;
		
		public MyStack1(){
			this.stackData = new Stack<Integer>();
			this.stackMin  = new Stack<Integer>();
		}
		
		public void push(int newNum){
			if (this.stackMin.isEmpty()){
				this.stackMin.push(newNum);
			}
			else if (newNum <= this.getmin()){
				this.stackMin.push(newNum);
			}
			this.stackData.push(newNum);
		}
		
		public int pop(){
			if (this.stackData.isEmpty()){
				throw new RuntimeException("Your stack is empty");
			}
			int value = this.stackData.pop();
			if (value == this.getmin()){
				this.stackMin.pop();
				
			}
			return value;
		}
		
		public int getmin(){
			if (this.stackMin.isEmpty()){
				throw new RuntimeException("Your stack is empty");
				
			}
			return this.stackMin.peek();
		}
		
		public static void main(String[] args){
			MyStack1 s = new MyStack1();
			s.push(3);
			s.push(4);
			s.push(1);
			s.push(0);
			
			System.out.print(s.getmin());
		}
	}


### 1.2 两个栈组成的队列 ###

	package chapter1;
	import java.util.*;
	
	
	public class TwoStackQueue {
		public Stack<Integer> stackPush;
		public Stack<Integer> stackPop;
		
		public TwoStackQueue(){
			stackPush = new Stack<Integer>();
			stackPop  = new Stack<Integer>();
			
		}
		
		public void add(int pushInt){
			stackPush.push(pushInt);		
		}
		
		public int poll(){
			if (stackPop.isEmpty() && stackPush.isEmpty()){
				throw new RuntimeException("Queue is empty");
				
			}
			else if (stackPop.isEmpty()){
				while (!stackPop.isEmpty()){
					stackPop.push(stackPush.pop());
				}
			}
			return stackPop.pop();
		}
		
		public int peek(){
			if (stackPop.isEmpty() &&  stackPush.isEmpty()){
				throw new RuntimeException("Queue is empty!");
			}
			else if (stackPop.isEmpty()){
				while (!stackPush.isEmpty()){
					stackPop.push(stackPush.pop());
				}
			}
			return stackPop.peek();
		}
	}


### 1.3 仅用递归函数和栈操作逆序一个栈 ###

	package chapter1;
	import java.util.*;
	
	
	public class Reverse {
		
		public static int getAndRemoveLastElement(Stack<Integer> stack){
			int result = stack.pop();
			if (stack.isEmpty()) {
				return result;
			}
			else {
				int last = getAndRemoveLastElement(stack);
				stack.push(result);
				return last;
			}
		}
		
		public static void reverse(Stack<Integer> stack){
			if (stack.isEmpty()) {
				return ;
			}
			int i = getAndRemoveLastElement(stack);
			reverse(stack);
			stack.push(i);
		}
		
		public static void main(String[] args){
			Stack<Integer> s1 = new Stack<Integer>();
			s1.push(2);
			s1.push(3);
			s1.push(4);
			s1.push(5);
			s1.push(6);
			s1.push(7);
			
			System.out.println(s1);
			Reverse.reverse(s1);
			System.out.print(s1);
		}
	}




### 1.5 用一个栈实现另一个栈的排序 ###

利用另一个栈将一个栈中元素为整数类型的栈进行从大到小排序。
将要排序的栈记为stack，申请的辅助栈记为help。stack执行pop操作，弹出的元素记为cur。

- 如果cur小于help栈顶的元素，直接将cur压入help栈中；
- 如果cur大于help栈顶的元素，先将help中元素逐一弹出，直到cur小于或等于help的栈顶元素，再将cur压入help。

源程序如下：

	package chapter1;
	import java.util.*;
	
	public class SortStackByStack {
		
		public static void sortStackByStack(Stack<Integer> stack) {
			Stack<Integer> help = new Stack<Integer>();
			while (!stack.isEmpty()) {
				int cur = stack.pop();
				while (!help.isEmpty() && help.peek() > cur) {
					stack.push(help.pop()) ;
				}
				help.push(cur) ;
			}
			
			// 将排序好之后的元素全部重新压入到stack栈中，从大到小排序；
			while (!help.isEmpty()) {
				stack.push(help.pop()) ;
			}
		} 
		
	//	测试
		public static void main(String[] args){
			Stack<Integer> s = new Stack<Integer>();
			s.push(3);
			s.push(2);
			s.push(8);
			s.push(4);
			s.push(9);
			
			System.out.println(s);
			SortStackByStack.sortStackByStack(s);
			System.out.print(s);
		}
	}

输出： 

	[3, 2, 8, 4, 9]
	[9, 8, 4, 3, 2]





















































































































































































































































































