Given an integer array nums of size n. Return all elements which appear more than n/3 times in the array. The output can be returned in any order.

imp:
isme aisa bhi ho sakta hai ki majority element ho hi na

approach:
MOORE VOTING ALGO :
how many majority elemnts for n/3 ???? ans: 2 for n/4 -:3
reason: agar n/3+n/3+n/3 =n then shuruat ke do elemnts hi n/3 se badhe honge tessra chota hi hoga since total to n hi hai

Initialize four variables: cnt1 and cnt2 for tracking the counts of elements, and el1 and el2 for storing the potential majority elements.
Traverse through the given array:
If cnt1 is 0 and the current element is not equal to el2, set el1 to the current element and increment cnt1 by 1.
If cnt2 is 0 and the current element is not equal to el1, set el2 to the current element and increment cnt2 by 1.
If the current element is equal to el1, increment cnt1 by 1.
If the current element is equal to el2, increment cnt2 by 1.
In all other cases, decrease cnt1 and cnt2 by 1.
After processing all elements, el1 and el2 should be the candidate elements for majority. To confirm:
Use another loop to manually check the counts of el1 and el2 in the array.
If either el1 or el2's count is greater than floor(N/3), it is considered a valid majority element.

same code as moore algo in n/2 we had only one majority so ek counter and el element yhan do hai so do cntr and do elemets and additionally include el2 != nums[i] so that dono ele1 and e;le2 same number ko majority maane

class Solution {
public:
     vector<int> majorityElement(vector<int>& nums) {
            
        int n = nums.size(); 

        int cnt1 = 0, cnt2 = 0;
        int el1 = INT_MIN, el2 = INT_MIN;

        for (int i = 0; i < n; i++) {
            
            if (cnt1 == 0 && el2 != nums[i]) {
                cnt1 = 1;
                el1 = nums[i]; 
            }
            else if (cnt2 == 0 && el1 != nums[i]) {
                cnt2 = 1;
                el2 = nums[i]; 
            } 
            else if (nums[i] == el1) {
        
                cnt1++;
            } 
            else if (nums[i] == el2) {
            
                cnt2++; 
            } 
            else {
                
                cnt1--; 
         
                cnt2--;
            }
        }
        cnt1 = 0, cnt2 = 0; 
        
        for (int i = 0; i < n; i++) {
            if (nums[i] == el1) {
                cnt1++; 
            }
            if (nums[i] == el2) {
            
                cnt2++;
            }
        }

        int mini =(int) n / 3 + 1;
        
        vector<int> result; 

        if (cnt1 >= mini) {
            result.push_back(el1);
        }
        if (cnt2 >= mini && el1 != el2) {

            result.push_back(el2); 
        }

        return result;
    }
};
Why el2 != nums[i] ?

We must avoid assigning the same number to both candidates.

Without this condition, something like this could happen.

Example:

nums = [2,2,2]

Step 1

cnt1 = 0 → el1 = 2

Step 2

If we didn't check el2 != nums[i], then

cnt2 = 0 → el2 = 2

Now both candidates become:

el1 = 2
el2 = 2

Which is wrong, because the algorithm is supposed to track two different candidates.
        
