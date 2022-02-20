# Today I Learned

> ## 알고리즘

### O(n^2)인 것

#### 삽입 정렬

```c
//C++
void insertion(int *array, int begin, int end)
{
	for (int i = begin + 1; i <= end; i++)
	{
		int j, v = array[i];
		for (j = i; j > begin && array[j - 1] > v; j--)
			array[j] = array[j - 1];
		if (i != j) array[j] = v;
	}
}
```



```python
#python

def insertion(lst):
    n = len(lst)
    for i in range(1,n):
        x = lst[i]
        while i > 0 and lst[i - 1] > x:
            lst[i] = lst[i - 1]
            i -= 1
        lst[i] = x
    return lst
```



#### 이진삽입정렬

```c
//C++
void binary_insertion(int *array, int begin, int end)
{
    for (int i = begin + 1; i <= end; i++)
    {
        int v = array[i], f = begin, l = i - 1;
        while (f <= l)
        {
            int m = (f + l) / 2;
            if (array[m] > v)
                l = m - 1;
            else
                f = m + 1;
        }
        for (l = i; l > f; l--)
            array[l] = array[l - 1];
        array[f] = v;
    }
}
```



## O( n log n)인 것

### 병합정렬

```c
#include <vector>

void merge(int *array, int begin, int end)
{
    if(begin < end)
    {
        int left_pivot = (begin + end) / 2;
        int right_pivot = left_pivot + 1;

        //Divide
        if (begin != left_pivot)
        {
            merge(array, begin, left_pivot);
            merge(array, right_pivot, end);
        }

        //Conquer
        std::vector<int> temp(end - begin + 1);
        int first_division = begin;
        int second_division = right_pivot;
        int i=0;

        while (first_division <= left_pivot && second_division <= end)
        {
            if (array[first_division] <= array[second_division])
            {
                temp[i++] = array[first_division++];
            }
            else
            {
                temp[i++] = array[second_division++];
            }
        }

        if (first_division > left_pivot)
        {
            while (second_division <= end)
            {
                temp[i++] = array[second_division++];
            }
        }
        else
        {
            while (first_division <= left_pivot)
            {
                temp[i++] = array[first_division++];
            }
        }

        for (i = begin; i <= end; ++i)
        {
            array[i] = temp[i - begin];
        }
    }
}
```



### 힙 정렬

```c
#include <algorithm>

using namespace std;

void heapify(int *array, int index, int size)
{
	for (int ch = (index << 1) | 1; ch < size; index = ch, ch = ch << 1 | 1)
	{
		if (ch + 1 < size && array[ch + 1] > array[ch]) ++ch;
		if (array[ch] <= array[index]) return;
		swap(array[ch], array[index]);
	}
}

void heap(int *array, int begin, int end)
{
	int *base = array + begin;
	int size = end - begin + 1;
	for (int i = size / 2 - 1; i >= 0; i--)
		heapify(base, i, size);

	while (--size >= 1)
	{
		swap(base[0], base[size]);
		heapify(base, 0, size);
	}
}
```



### 퀵 정렬

```c
#include <algorithm>

using namespace std;

void quick(int *array, int left, int right)
{
    int pivot = left;
    int left_pivot = left;
    int right_pivot = right;
    
    while (left_pivot < right_pivot)
    {
        while (array[left_pivot] <= array[pivot] && left_pivot < right)
        {
            left_pivot += 1;
        }
        
        while (array[right_pivot] >= array[pivot] && right_pivot > left)
        {
            right_pivot -= 1;
        }
        
        if (left_pivot < right_pivot)
        {
            swap(array[left_pivot], array[right_pivot]);
            
            continue;
        }

        swap(array[pivot], array[right_pivot]);
        quick(array, left, right_pivot - 1);
        quick(array, right_pivot + 1, right);
    }
}
```

