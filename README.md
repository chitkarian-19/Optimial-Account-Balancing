# Optimial-Account-Balancing
Minimize Cash Flow among a given set of friends who have borrowed money from each other

Well it's a coding problem which asks for minimum no of transactions, the problem solution tries to reduce the transactions.
let's say x is giving 100 rs to y and y is giving 100 rs to z, from naive appraoch it looks like first x has to give y and then y has to give the same amount to z.
It turns out that there are 2 transactions happening but we can reduce the transactions from 2 to 1 by directly allowing x to give the amount to z.
This approach will reduce the transaction from number 2 to 1.

Solution: it's a solved via greedy approach, first we will check that what is the total amount will be credited and debited from every person's account, After that we will check that where min amount and max amount is present, the min amount is the definitely the amount that will be debited and that's why it will be negative and vice versa goes for max amount.

After that we will check that what is the min of min amount and max amount by considering the absolute values.
We will substract the min from the amount array at the index where the amount was credited and we will add the min value to amount array at the index where the amount was going to be debited.
We will recursively do it until both the min and max index does not gets same.
I am sharing the code here, the source of question is at:

https://leetcode.com/discuss/interview-question/542341/amazon-onsite-minimum-transaction. <br/>
https://www.geeksforgeeks.org/minimize-cash-flow-among-given-set-friends-borrowed-money/



import java.io.*;

class GFG {
	public static void main (String[] args) {
		
		int graph[][] = { {0, 1, 1000},
                            {0, 2, 2000},
                            {1, 2, 5000},};
     
        // Print the solution
        minCashFlow(graph,3);
		
	}
	public static void minCashFlow(int[][] graph,int n){
	    int[] amount = new int[n];
	    java.util.Arrays.fill(amount,0);
	    for(int i=0;i<graph.length;i++){
	        int source = graph[i][0];
	        int dest = graph[i][1];
	        int cost = graph[i][2];
	        
	        amount[source]-=cost;
	        amount[dest]+=cost;
	        
	    }
	    
	    recur(amount,n);
	    
	}
	public static void recur(int[] amount,int n){
	    
	    int max_id = findMax(amount,n);
	    int min_id = findMin(amount,n);
	    if(max_id == min_id)
	     return ;
	    int min = Math.min(amount[max_id],-amount[min_id]);
	    
	    amount[min_id]+=min;
	    amount[max_id]-=min;
	    
	    System.out.println("Person "+min_id +" pays "+min+" to person "+max_id);
	    
	    recur(amount,n);
	}
	
	public static int findMin(int[] amount , int n){
	    int id =0;
	    for(int i=1;i<n;i++){
	        if(amount[i]<amount[id]){
	            id = i;
	        }
	    }
	    return id;
	}
		public static int findMax(int[] amount , int n){
	    int id =0;
	    for(int i=1;i<n;i++){
	        if(amount[i]>amount[id]){
	            id = i;
	        }
	    }
	    return id;
	}
	
}



