[42. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/)
(HARD)
Intuition -  find the right max element and left max element and apply this formula =  min(rightmax , leftmax)-height. 
```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        int n =height.size();
        if (n == 0) return 0;
        vector<int> leftmax(n);
        leftmax[0] = height[0];
        for(int i=1;i<n;i++){
            leftmax[i] = max(leftmax[i-1],height[i]);
        }
        vector<int> rightmax(n);
        rightmax[n-1] = height[n-1];
        for(int i=n-2;i>=0;i--){
            rightmax[i] = max(rightmax[i+1],height[i]);
        }
        int ans=0;
        for(int i=0;i<n;i++){
            int sum = min(leftmax[i],rightmax[i])-height[i];
            if(sum>0) ans+=sum;
        }
        return ans;
    }
};
```
[11. Container With Most Water](https://leetcode.com/problems/container-with-most-water/)
#twopointer
Intuition - Use two pointers and find min and multiply with  length.
```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        int n = height.size();
        int left = 0;
        int right = n-1;
        int maxi =0;
        while(left<right){
            maxi = max(min(height[left],height[right])*(right-left),maxi);
            if(height[left]>height[right]){
                right--;
            }
            else {
                left++;
            }
        }
        return maxi;
    }

};
```

[853. Car Fleet](https://leetcode.com/problems/car-fleet/)
#math #greedy #sorting
Intuition  -   first we need to calculate the time going to take to reach the target and sort them on the basis of their position where they start in descending order. the position which is greater should be above. After that count++ when ever we have a car which's time to reach is greater than the previous a new fleet if its less are equal than the previous its means the previous and this will start a fleet 
```cpp
class Solution {
public:
    static bool comp(const pair<int,double>& a,const pair<int,double>& b){
        return a.first>b.first;
    }
    int carFleet(int target, vector<int>& position, vector<int>& speed) {
        vector<pair<int,double>> cars;
        int n = position.size();
        for(int i=0;i<n;i++){
            cars.push_back({position[i],(double)(target-position[i])/speed[i]});
        }
        sort(cars.begin(),cars.end(),comp);
        int count = 0;
        double prev = 0.0;
        for(auto car:cars){
            if(car.second>prev){
                count++;
                prev = car.second;
            }
        }
        return count;
    }
};
```


