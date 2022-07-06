# 零、准备工作

```c++
int main() {
	vector<int> vec{ 1,2,3,5,6 };
	int len = vec.size();
	for (int i = 0; i < len; i++) {
		cout << vec[i] << " ";
	}
	cout << endl;
	cout << "要查找的数值为：";
	int val;
	cin >> val;
	cout << erfen_last_small(vec, val) << endl;
}
```



# 一、查找函数

## 1.等于val的数字下标

```c++
int erfen(vector<int> vec, int val) {
	int len = vec.size() - 1;
	int left = 0;
	int right = len;
	while (left <= right) {
		int mid = left + ((right - left) >> 1);
		if (val == vec[mid]) return mid;
		else if (val > vec[mid]) left = mid + 1;
		else right = mid - 1;
	}
	return -1;
}
```



## 2.第一个等于val的数字下标

```c++
int erfen_first_equal(vector<int> vec, int val) {
	int len = vec.size();
	int left = 0;
	int right = len - 1;
    
	while (left <= right) {
		int mid = left + ((right - left) >> 1);
		if (val == vec[mid]) right = mid - 1;
		else if (val > vec[mid]) left = mid + 1;
		else right = mid - 1;
	}

	//必须判断left < len，要不然查找大于数组最大值的数的时候越界。
	if (left < len && vec[left] == val) return left; 
	return -1;
}
```



## 3.最后一个等于val的数字下标

```c++
//和erfen_first_equal反着来就行
int erfen_last_equal(vector<int> vec, int val) {
	int len = vec.size();
	int left = 0;
	int right = len - 1;
    
	while (left <= right) {
		int mid = left + ((right - left) >> 1);
		if (val == vec[mid]) left = mid + 1;
		else if (val > vec[mid]) left = mid + 1;
		else right = mid - 1;
	}

	//必须判断right >= 0，要不然查找小于数组最小值的数的时候越界。
	if (right >= 0 && vec[right] == val) return right;
	return -1;
}
```



## 4.第一个大于等于val的数字下标

```c++
int erfen_first_large_equal(vector<int> vec, int val) {
	int len = vec.size();
	int left = 0;
	int right = len - 1;
    
	while (left <= right) {
		int mid = left + ((right - left) >> 1);
		if (val == vec[mid]) right = mid - 1;
		else if (val > vec[mid]) left = mid + 1;
		else right = mid - 1;
	}
    
	if (left < len) return left;
	return -1;
}
```



## 5.最后一个小于等于val的数字下标

```c++
//和erfen_first_large_equal反过来就行
int erfen_last_small_equal(vector<int> vec, int val) {
	int len = vec.size();
	int left = 0;
	int right = len - 1;
    
	while (left <= right) {
		int mid = left + ((right - left) >> 1);
		if (val == vec[mid]) left = mid + 1;
		else if (val > vec[mid]) left = mid + 1;
		else right = mid - 1;
	}
    
	if (right >= 0) return right;
	return -1;
}
```



## 6.第一个大于val的数字下标

```c++
int erfen_first_big(vector<int> vec, int val) {
	int len = vec.size();
	int left = 0;
	int right = len - 1;
    
	while (left <= right) {
		int mid = left + ((right - left) >> 1);
		if (val == vec[mid]) left = mid + 1;
		else if (val > vec[mid]) left = mid + 1;
		else right = mid - 1;
	}

	//和erfen_last_small_equal相比，改这行就行
	if (left < len) return left;
	return -1;
}
```



## 7.最后一个小于val的数字下标

```c++
int erfen_last_small(vector<int> vec, int val) {
	int len = vec.size();
	int left = 0;
	int right = len - 1;
    
	while (left <= right) {
		int mid = left + ((right - left) >> 1);
		if (val == vec[mid]) right = mid - 1;
		else if (val > vec[mid]) left = mid + 1;
		else right = mid - 1;
	}

	//和erfen_last_small_equal相比，改这行就行
	if (right >= 0) return right;
	return -1;
}
```



# 二、区别

|      |            | val==mid时的操作 |           return 条件           | return |
| :--: | :--------: | :--------------: | :-----------------------------: | :----: |
|  1   |     =      |    return mid    |                /                |  mid   |
|  2   |  第一个=   | right = mid - 1  | left < len && vec[left] == val  |  left  |
|  3   | 最后一个=  |  left = mid + 1  | right >= 0 && vec[right] == val | right  |
|  4   |  第一个>=  | right = mid - 1  |           left < len            |  left  |
|  5   | 最后一个<= |  left = mid + 1  |           right >= 0            | right  |
|  6   |  第一个>   |  left = mid + 1  |           left < len            |  left  |
|  7   | 最后一个<  | right = mid - 1  |           right >= 0            | right  |



# 三、模板

下面的模板是上述2-7函数的模板。

在草稿纸上做一个数组演示一下就行。

```c++
int function_name(vector<int> vec, int val) {
	int len = vec.size();
	int left = 0;
	int right = len - 1;
    
	while (left <= right) {
		int mid = left + ((right - left) >> 1);
        
        //处理条件为right = mid - 1或者left = mid + 1
		if (val == vec[mid]) 处理;
		else if (val > vec[mid]) left = mid + 1;
		else right = mid - 1;
	}

	//返回条件为left < len && vec[left] == val或者right >= 0 && vec[right] == val
    //返回值为left或者right
	if (返回条件) return 返回值;
    
	return -1;
}
```





















