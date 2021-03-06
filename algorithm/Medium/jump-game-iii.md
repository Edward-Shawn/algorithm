﻿# algorithm 
1306. Jump Game III
  
arr라는 배열이 주어지면 n개의 점프 파워가 적혀있다. +, - 방향으로 점프를 하면서  
arr 요소 0인 요소로 도달 할 수 있는 인덱스가 존재하는지 판별하는 스크립트 제작이다.  
이전에 다른 코딩면접 때 본 적 있는 문제이다.  
  
# 문제 링크    
https://leetcode.com/problems/jump-game-iii/


![title](https://github.com/jungmin3834/algorithm/blob/master/image/jump-game-iii.png)

# 코드  

재귀함수 솔루션  
```cpp

class Solution {
public:
bool searchReach(vector<bool>& veclist , vector<int>& arr , int start , int size)
{
	if (veclist[start] == true)
		return false;
	else if (arr[start] == 0)
		return true;
	
		veclist[start] = true;
    
	if (start + arr[start] < size && searchReach(veclist, arr, start + arr[start], size) == true)
		return true;
	if (start - arr[start] > -1 && searchReach(veclist, arr, start - arr[start], size) == true)
		return true;
    
	return false;
}


bool canReach(vector<int>& arr, int start) {

	int size = arr.size();
	vector<bool> veclist = vector<bool>(size, false);
	return searchReach(veclist, arr, start,arr.size());
}
};

```

재귀 없이 제작한 솔루션   
```cpp

class Solution {
public:
    bool canReach(vector<int>& arr, int start) {
    
    int size = arr.size();
	vector<bool> veclist = vector<bool>(size, false);
	queue<int> que = queue<int>();
	que.push(start);
	
	while (que.size() != 0)
	{
		int n = que.front(); que.pop();
		if (veclist[n] == true)
			continue;
		else if (arr[n] == 0)
			return true;
		
		veclist[n] = true;
		int step = arr[n];

		if (n + step < size)
			que.push(n + step);
		if (n - step > -1)
			que.push(n - step);
	}
	return false;
    }
};

```
