# Leetcode 1168. Optimize Water Distribution in a Village

[Explanation Video Link on Youtube](https://youtu.be/iLfiGrvkheE)

[B站英文解说视频链接](https://www.bilibili.com/video/BV1RQ4y1k7i9?share\_source=copy\_web)

```cpp
class Solution {
public:
    int minCostToSupplyWater(int n, vector<int>& wells, vector<vector<int>>& pipes) {
        priority_queue<tuple<int, int, int>, vector<tuple<int, int,int>>, greater<tuple<int, int, int>>> pq;
        
        for (int i = 0; i < wells.size(); i++) {
            pq.emplace(make_tuple(wells[i], 0, i + 1));
        }
        
        for (int i = 0; i < pipes.size(); i++) {
            pq.emplace(make_tuple(pipes[i][2], pipes[i][0], pipes[i][1]));
        }
        
        for (int i = 0; i <= n; i++) {
            parents.push_back(i);
        }
        
        int res = 0;
        
        while (n) {
            auto [first, second, third] = pq.top();
            pq.pop();
            int pa = find_parent(second);
            int pb = find_parent(third);
            
            if (pa != pb) {
                parents[pb] = pa;
                n--;
                res += first;
            }
        }
        
        return res;
    }
    
    int find_parent(int node) {
        if (node != parents[node]) {
            parents[node] = find_parent(parents[node]);
        }
        
        return parents[node];
    }
    
private:
    vector<int> parents;
};
```
