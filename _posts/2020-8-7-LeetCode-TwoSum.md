---
layout: post
title: '[LeetCode] easy : Two Sum'
---

## 풀이

여러 시간복잡도로 풀어볼 수 있는 좋은 문제라고 생각한다.
일단 문제보자마자 2중반복으로 전체탐색을 해보면 512ms정답을 얻을 수 있었다. O(n^2)
그리고 sorting을 한 후 이분탐색으로 접근을 하면 조금 더 좋은 답을 얻을 수 있다. O(nlogn)

숫자의 범위가 안나와있어서 메모이제이션으로 O(n)으로 풀어보려고 헀는데 런타임에러가 역시 나더라.
그래서 map을 사용해서 16ms를 얻을 수 있었다. O(n)
정렬을 수행안하는 unordered_map은 해싱기반이라 O(n)이다.

이풀이가 상위15%이므로 더좋은 풀이도 존재한다.
아마 unordered_map을 해싱처럼 사용을 하거나 직접 큰소수만큼 해시테이블잡고 계산하면 더 빠를것같다.

내풀이는 그냥 메모이제이션 처럼
unordered_map 2개를  nums[i]:빈도 , nums[i]:마지막idx 로 키밸류쌍을 잡아주고 값을 넣어준 다음에 
같은수 2개가 정답이 되는 예외처리만 해주고 map.count로 정답을 접근해 값을 바로 찾아보는 방식이다.


## 코드

```cpp
LeetCode - Two Sum


class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {

      ios_base::sync_with_stdio(false);
	    cin.tie(NULL);
	    cout.tie(NULL);

        //nums[i] , key숫자나온횟수
        unordered_map<int,int> m;
        //nums[i], 해당숫자 마지막 idx
        unordered_map<int, int > m_idx;
        
        vector<int> sol;
        
        //map에 nums넣기
        for(int i=0;i<nums.size();i++){
            if (m.count(nums[i]) == 0) {
			    m[nums[i]] = 1;
		    }
		    else {
			    m[nums[i]] = m[nums[i]] + 1;
		    }
		    m_idx[nums[i]] = i;
        }   
        
        for(int i=0;i<nums.size();i++){
            int tmp = target - nums[i];
		    //같은수 2개 엘리먼트가 답을 만드는경우
		    if (tmp == nums[i]) {
			    if (m.count(tmp)>0 && m[nums[i]] < 2) {
				    //2개미만이면 답이되지않음.
				    continue;
			    }
		    }

		    //정답을 발견한 경우
		    if (m.count(tmp) > 0) {
			    sol.push_back(i);
			    sol.push_back(m_idx[tmp]);
                break;
		    }
        }
        
        return sol;
    }
};
```
