# SUBMISSION IS ALL U NEED 

*********************************************************************************************************************************

                                                A. Submission is All You Need
time limit per test1 second
memory limit per test256 megabytes
For a multiset 𝑇
 consisting of non-negative integers, we define:

sum(𝑇)
 is the sum of all elements in 𝑇
. For example, if 𝑇={0,1,1,3}, then sum(𝑇)=0+1+1+3=5


mex(𝑇) is the smallest non-negative integer not in 𝑇
. For example, if 𝑇={0,1,1,3}, then mex(𝑇)=2
 because 2 is the smallest non-negative integer not present in 𝑇.
You are given a multiset 𝑆
 of size 𝑛
 consisting of non-negative integers. At first, your score is 0
. You can perform the following operations any number of times in any order (possibly zero):
Select a subset 𝑆′⊆𝑆
 (i.e., 𝑆′
 contains some of the elements currently in 𝑆
), add sum(𝑆′)
 to your score, and then remove 𝑆′
 from 𝑆
.
Select a subset 𝑆′⊆𝑆
, add mex(𝑆′)
 to your score, and then remove 𝑆′
 from 𝑆
.
Find the maximum possible score that can be obtained.

## Input
Each test contains multiple test cases. The first line contains the number of test cases 𝑡
 (1≤𝑡≤103
). The description of the test cases follows.
The first line of each test case contains a single integer 𝑛
 (1≤𝑛≤50
).
The second line of each test case contains 𝑛
 integers 𝑆1,𝑆2,…,𝑆𝑛
 (0≤𝑆𝑖≤50
).

## Output
For each test case, print a single integer — the MAXIMUM possible score that can be obtained.

*********************************************************************************************************************************


* a multiset is a set in which the elements can be repeated 
so we can also say that it a normal array

* initially our score is 0
* we can perform two operations :
        1. take a subset if the multiset ---> then take sum(subset) ---> remove that subset from multiset
        2. take a subset if the multiset ---> then take mex(subset) ---> remove that subset from multiset

mex value being the smallest non-negative integer not present in the set.
as for each test case we need to print the maximum possible score that can be obtained.
we have two cases either add the sum which in most cases will be greater then mex value with exceptions being
mex(subset(0)) ---> 1 where the sum (subset(0)) ----> 0 

suppose S = <0,1>
mex(S) = ans + 2
sum(S) = ans + 1

all the subsets after <0,1> will have (sum value > mex value) like <0,1,2> and so on
so what we can see whenever we find <0,1, x,y,z> etc
we take value 2 for mex(0,1) and for the rest if values are 0 take 1
or else add the values


* example <0,0,0,1> = 2+1+1 = 4
* example <0,1,3,5,0,0,1> = 3+5+2+2+1 = 13
* also lets say that #Zeros = 10 & #Ones = 7, here we take the min of #(zeroes && ones) multiply it with 2 and then add 1 acc to remaining # 
same for  #Zeros = 7 & #Ones = 10



## CODE:  (pure standard C++ (no GCC-only headers like <bits/stdc++.h> ---------> use GNU g++ 13.2))

#####################################################################################################################
```cpp
#include <iostream>
using namespace std;

void solve() {
    int n;
    cin >> n;
    int score = 0;
    int temp;
    for (int i = 0; i < n; i++) {
        cin >> temp;
        if (temp == 0) 
            score++;
        else 
            score += temp;
    }
    cout << score << '\n';
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    int t;
    cin >> t;
    while (t--) {
        solve();
    }
    return 0;
}
```
#####################################################################################################################
* okay so coming the above code and why it works in comparison to the below code 
* this code follows a simple rule, before that lets say we have S = <0,1,1>
* according to the logic of above logic 
* for i = 0 ->> ans++;
* for i !=0 ->> ans+= i;

* now lets take an example S  <0,1,1>
* now lets solve it in 2 ways
1. pair #0 ans #1 together then ans = 2+1= 3
2. without pairing ans = for 0 -> add 1 (mex) , for 1-> add 1(sum) = 1+1+1 =3
   and hence in both situations we receive the same answer just by pairing we consider the pair and multiply them by 2 in the below code 
   whereas in the upper by we dont need to multiply by 2 as they already give the same summation answer.

### the above code worked 
### the below code of mine did'nt work

for {0} we always take mex cause it gives us 1
for {1} we always take sum cause it gives 1 too 
ans as we need max


#####################################################################################################################
```cpp
* #include<bits/stdc++.h> 
* using namespace std;
* #define ll long long
* int main(){
*    ll t, n, i, j, z, o, ans; 
*    cin >> t;
*    // t -> test cases
*    for(;t--;){
        cin>>n; // size of array input 
        ans=z=o=0;
        ll a[n]; // initialized the size of array
        for(i=0;i<n;i++){
            cin >> a[i];
            if(a[i]==0) z++;
            else if (a[i]==1) o++;
            ans = ans + a[i]; //  added the values of all elements (diff values + no of ones)
            }
            ans = ans + min(z,o)*2 -min(z,o); // important
            //min(z,o)*2 works on basis of no of 0's 
            //-min(z,o) will remove the excess ones
            // as the total no of ones is already added
            //and the ones paired with 0 will be mul by 2
            if(z>0){ // major mistake
            if(z>o){ //now correct
                //if #o's greater than 1 should be added that many times
                ans = ans + z-o;
          }
            cout<< ans << endl;
     }
* }
```
#####################################################################################################################
for this I were basically thinking like this:
Pair each 0 with a 1.
Multiply that 1 by 2 (bonus).
Subtract the “excess” 1s so they don’t double count.

n = 3
a = [0, 1, 1]

Your thinking:
Pair (0,1) → that 1 becomes 2.
Keep the other 1.
Result = 3.

But your implementation did:
The extra correction step + (z - o) is the killer. You thought it’s balancing, but actually it destroys the count when o > z.

okay okayyyyyyy
so i figured the problem 
we can solve the problem with bith of the codes the problem was i wrote the condition as if(z>0)
when it should have been if(z>o) and now it got accepted .


so yeah this is done.