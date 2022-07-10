10th July LC Contest 301:

o/p: only 1 out of 4 Qs tried but not fully solved


solution to 1 Q: looke dliek DP problem

class Solution {
public:
    int fillCups(vector<int>& amount) {
        int cold=amount[0]; // cold water to be filled in these many cups
        int warm =amount[1]; // warm 
        int hot=amount[2]; // hot
        vector<int> reducedCups(amount);  //copy of original vector
        unordered_map<string, int> dp;
        
        //base case
        if (amount[0]==0 && amount[1]==0 && amount[2]==0) return 0; // [0,0,0]
        if (amount[0]==1 & amount[1]==1 && amount[2] ==1) return 2; // [1,1,1]
        if (amount[0]+amount[1]+amount[2]==amount[0] || 
            amount[0]+amount[1]+amount[2]==amount[1] || 
            amount[0]+amount[1]+amount[2]==amount[2] ) return amount[0]+amount[1]+amount[2]; // two of the elements are zero
        if ((cold!=1 && warm==1 && hot ==1) || 
            (cold==1 && warm !=1 && hot ==1)|| 
            (cold ==1 && warm ==1 && hot !=1))  return 1 +(cold+warm+hot -2); //two of the elements are 1 and 3rd is not 1(0 or >1)
        
        //sort vector
        sort(amount.begin(),amount.end(), greater<int>()); // decreasing order
        //in 1 sec fill 2 cups with diff water types
        reducedCups[0]--;
        reducedCups[1]--;
        //string key1= itoa(reducedCups[0])+itoa(reducedCups[1]) + itoa(reducedCups[2]);
       // if dp[key1] !==NULL   /// key exists in unorderred_map? without overflowing dp indexx limit ?????????? How to do
        int ans1=fillCups(reducedCups);
         //dp.push_back(make_pair(key, ans1))
        //alt: in 1 sec fill 1 cup with 1 type of water
        //int i=max(reducedCups[0], reducedCups[1]. reducedCups[2]);
        sort(reducedCups.begin(), reducedCups.end(), greater<int>());
        reducedCups[0]--;
        
        //string key2= itoa(reducedCups[0])+itoa(reducedCups[1]) + itoa(reducedCups[2]);
        int ans2=fillCups(reducedCups);
        //dp.push_back(make_pair(key2, ans2));
        
        return  ans1 + ans2;
    }
};


Qs faced and googled: 
- [X] create a vector of size n in c++.  .. https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/
- [ ] how to sort vector in c++ in descending order. ... https://www.geeksforgeeks.org/how-to-sort-a-vector-in-descending-order-using-stl-in-c/
- [ ] create a copy of a vector c++. ... https://www.geeksforgeeks.org/ways-copy-vector-c/      https://www.techiedelight.com/copy-vector-cpp/
- [ ] What data types are allowed as key of a unorderred_map, map?
- [ ] How to check if an item exists in map without exceeding its index if using indexx access method

