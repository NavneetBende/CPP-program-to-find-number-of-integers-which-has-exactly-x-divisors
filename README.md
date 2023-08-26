# CPP-program-to-find-number-of-integers-which-has-exactly-x-divisors

Number of integers which has exactly x divisors in C++
 
Numbers dividing with self or 1 are called prime numbers but numbers having multiple divisors are called composite numbers. In this c++ program, we will find the numbers with the exact number of divisors defined by the user. The divisor of a number is defined as, when we divide a number ‘a’ by other number ‘b’ and gives remainder zero, so the ‘b’ will be considered as the divisor of the ‘a’.
Number of integers which has exactly x divisors in C++
Here, in this page we will discuss the two different ways for finding the required count of numbers that have exactly x divisors. These two methods are given below,

Method 1 : Naive approach
Method 2 : Efficient approach
Method 1 :
Declare a variable count =0, to count the required numbers with x factors.
Run a loop for range 1 to n.
Inside that take a variable count_factors = 0, that will count the factors of ith.
Now, run a inner loop.
And increase the count_factors if it’s is factor of ith number.
Check if count_factors == X, then increment the count by 1.
At last print the count value.
Method 1 : Code in C++
Run
//Write a program to count Number of integers which has exactly X divisors in C++
#include<iostream>
#include<math.h>
using namespace std;

int main(){
    
    int n=7, x=2;
    
    //Variable of count required numbers
    int count = 0;
    
    for(int i=1; i<=n; i++){
        
        //variable to count the factors of i-th number
        int count_factors = 0;
        for(int j = 1; j<=sqrt(i); j++){
            if(i%j==0){
                if(i/j != j)
                    count_factors += 2;
                else
                    count_factors++;
            }
        }
        
        if(count_factors == x)
            count++;
    }
    
    cout<<count;
}
Output :
4
Related Pages
Counting number of days in a given month of a year
 
Finding Number of times x digit occurs in a given input
 
Finding Roots of a quadratic equation

Power of a Number 

Prime Number

Method 2 :
In this method we will use the efficient way for counting the factors that used in method 1. We use the sieve of eratosthenes for counting the factors.

Method 2 : Code in C++
Run
//Write a program to count Number of integers which has exactly X divisors in C++
#include<bits/stdc++.h>
using namespace std;
 
// function for sieve of eratosthenes
void sieve(bool primes[], int x)
{
    primes[1] = false;
 
    for (int i=2; i*i <= x; i++)
    {
        if (primes[i] == true)
        {
            for (int j=2; j*j <= x; j++)
                primes[i*j] = false;
        }
    }
}
 
int nDivisors(bool primes[], int x, int a, int b, int n)
{

    int result = 0;
 
    vector<int>  v;
    for (int i = 2; i <= x; i++)
        if (primes[i] == true)
            v.push_back (i);
 
    for (int i=a; i<=b; i++)
    {
        int temp = i;
 
        int total = 1;
        int j = 0;
 
        for (int k = v[j]; k*k <= temp; k = v[++j])
        {
            int count = 0;
 
            while (temp%k == 0)
            {
                count++;
                temp = temp/k;
            }
 
            total = total*(count+1);
        }
 
        if (temp != 1)
            total = total*2;
 
        if (total == n)
            result++;
    }
    return result;
}
 
int countNDivisors(int a, int b, int n)
{
    int x = sqrt(b) + 1;
 
    bool primes[x];
 
    memset(primes, true, sizeof(primes));
    sieve(primes, x);
 
    return nDivisors(primes, x, a, b, n);
}
 

int main()
{
    int a = 1, b = 7, n = 2;
    cout << countNDivisors(a, b, n);
    return 0;
}
Output :
4
