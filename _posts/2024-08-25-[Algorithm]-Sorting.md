---
layout: post
date: 2024-08-25
title: "[Algorithm] Sorting"
tags: [Algorithm, Sorting, ]
categories: [Algorithm, Sorting, ]
---


### 1. **기본 정렬 알고리즘**


#### 1.1 버블 정렬 (Bubble Sort)

- **개념**: 인접한 두 요소를 비교하여 필요할 경우 교환하는 과정을 반복하는 단순한 정렬 알고리즘이다.
- **시간 복잡도**: O(n²)
- **특징**: 알고리즘이 단순하지만, 비효율적이기 때문에 실무에서는 거의 사용되지 않는다.


{% raw %}
```java
public void bubbleSort(int[] arr) {
    int n = arr.length;
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                // Swap arr[j] and arr[j + 1]
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}
```
{% endraw %}



#### 1.2 선택 정렬 (Selection Sort)

- **개념**: 배열을 순차적으로 탐색하여 가장 작은 요소를 찾아 맨 앞의 요소와 교환하는 정렬 알고리즘이다.
- **시간 복잡도**: O(n²)
- **특징**: 비교 횟수는 많지만 교환 횟수가 적어 버블 정렬보다는 효율적이다.


{% raw %}
```java
public void selectionSort(int[] arr) {
    int n = arr.length;
    for (int i = 0; i < n - 1; i++) {
        int minIdx = i;
        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIdx]) {
                minIdx = j;
            }
        }
        int temp = arr[minIdx];
        arr[minIdx] = arr[i];
        arr[i] = temp;
    }
}
```
{% endraw %}



#### 1.3 삽입 정렬 (Insertion Sort)

- **개념**: 배열을 순차적으로 탐색하며, 각 요소를 그보다 앞서 있는 정렬된 부분에 적절한 위치에 삽입하는 알고리즘이다.
- **시간 복잡도**: O(n²)
- **특징**: 데이터가 거의 정렬되어 있는 경우 매우 효율적이며, O(n) 성능을 보인다.


{% raw %}
```java
public void insertionSort(int[] arr) {
    int n = arr.length;
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
}
```
{% endraw %}



#### 2. **고급 정렬 알고리즘**


#### 2.1 병합 정렬 (Merge Sort)

- **개념**: 배열을 반으로 나누고, 각각을 정렬한 후 병합하는 방식의 정렬 알고리즘이다.
- **시간 복잡도**: O(n log n)
- **특징**: 안정 정렬이며, 재귀적으로 동작해. 공간 복잡도는 O(n)이다.


{% raw %}
```java
public void mergeSort(int[] arr, int l, int r) {
    if (l < r) {
        int m = (l + r) / 2;
        mergeSort(arr, l, m);
        mergeSort(arr, m + 1, r);
        merge(arr, l, m, r);
    }
}

public void merge(int[] arr, int l, int m, int r) {
    int n1 = m - l + 1;
    int n2 = r - m;

    int[] L = new int[n1];
    int[] R = new int[n2];

    for (int i = 0; i < n1; i++)
        L[i] = arr[l + i];
    for (int j = 0; j < n2; j++)
        R[j] = arr[m + 1 + j];

    int i = 0, j = 0;
    int k = l;
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k] = L[i];
            i++;
        } else {
            arr[k] = R[j];
            j++;
        }
        k++;
    }

    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }

    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}
```
{% endraw %}



#### 2.2 퀵 정렬 (Quick Sort)

- **개념**: 피벗을 기준으로 작은 요소와 큰 요소로 배열을 분할하고, 재귀적으로 정렬하는 알고리즘이다.
- **시간 복잡도**: 평균 O(n log n), 최악 O(n²)
- **특징**: 분할 정복 방식으로 동작하며, 제자리 정렬로 추가적인 메모리 공간이 거의 필요하지 않는다.


{% raw %}
```java
public int[] quickSort(int[] arr, int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
    return arr;
}

private int partition(int[] arr, int low, int high) {
    int pivot = arr[high];
    int i = (low - 1);
    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }
    }
    int temp = arr[i + 1];
    arr[i + 1] = arr[high];
    arr[high] = temp;
    return i + 1;
}
```
{% endraw %}



#### 2.3 힙 정렬 (Heap Sort)

- **개념**: 힙(우선순위 큐)를 이용하여 최대값 또는 최소값을 하나씩 추출하여 정렬하는 알고리즘이다.
- **시간 복잡도**: O(n log n)
- **특징**: 불안정 정렬이며, 추가 메모리 공간이 거의 필요하지 않는다.


{% raw %}
```java
public void heapSort(int[] arr) {
    int n = arr.length;
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(arr, n, i);
    for (int i = n - 1; i > 0; i--) {
        int temp = arr[0];
        arr[0] = arr[i];
        arr[i] = temp;
        heapify(arr, i, 0);
    }
}

void heapify(int[] arr, int n, int i) {
    int largest = i;
    int left = 2 * i + 1;
    int right = 2 * i + 2;
    if (left < n && arr[left] > arr[largest])
        largest = left;
    if (right < n && arr[right] > arr[largest])
        largest = right;
    if (largest != i) {
        int swap = arr[i];
        arr[i] = arr[largest];
        arr[largest] = swap;
        heapify(arr, n, largest);
    }
}
```
{% endraw %}



#### 3. **자바 내장 정렬 메서드**


#### 3.1 `Arrays.sort()`

- **기본형 배열**: 퀵소트를 기반으로 하는 Dual-Pivot Quicksort를 사용한다.
- **객체 배열**: Timsort 알고리즘을 사용하며, 안정 정렬이다.


{% raw %}
```java
int[] arr = {3, 1, 4, 1, 5, 9};
Arrays.sort(arr); // 오름차순 정렬
Arrays.sort(arr, Collections.reverseOrder()); // 내림차순 정렬 (Integer 배열에서만 가능)
```
{% endraw %}



#### 3.2 `Collections.sort()`

- **리스트 정렬**: 리스트를 정렬할 때 사용되며, Timsort 알고리즘을 사용한다.


{% raw %}
```java
List<Integer> list = Arrays.asList(3, 1, 4, 1, 5, 9);
Collections.sort(list); // 오름차순 정렬
Collections.sort(list, Collections.reverseOrder()); // 내림차순 정렬
```
{% endraw %}



#### 4. **정렬 알고리즘의 응용**


#### 4.1 K번째 최소/최대 원소 찾기

- 퀵 셀렉트(Quickselect) 알고리즘을 사용하거나 정렬 후 K번째 원소를 찾으면 된다.


{% raw %}
```java
public int quickSelect(int[] arr, int k) {
    return quick

SelectHelper(arr, 0, arr.length - 1, k - 1);
}

private int quickSelectHelper(int[] arr, int low, int high, int k) {
    if (low == high) {
        return arr[low];
    }

    int pivotIndex = partition(arr, low, high);
    if (k == pivotIndex) {
        return arr[k];
    } else if (k < pivotIndex) {
        return quickSelectHelper(arr, low, pivotIndex - 1, k);
    } else {
        return quickSelectHelper(arr, pivotIndex + 1, high, k);
    }
}
```
{% endraw %}



#### 4.2 두 배열의 합병 (Merge Two Sorted Arrays)

- 두 개의 정렬된 배열을 하나의 정렬된 배열로 병합할 때, 병합 정렬의 병합 단계와 유사한 알고리즘을 사용해.


{% raw %}
```java
public int[] mergeSortedArrays(int[] arr1, int[] arr2) {
    int n1 = arr1.length;
    int n2 = arr2.length;
    int[] result = new int[n1 + n2];
    int i = 0, j = 0, k = 0;

    while (i < n1 && j < n2) {
        if (arr1[i] <= arr2[j]) {
            result[k++] = arr1[i++];
        } else {
            result[k++] = arr2[j++];
        }
    }

    while (i < n1) {
        result[k++] = arr1[i++];
    }

    while (j < n2) {
        result[k++] = arr2[j++];
    }

    return result;
}
```
{% endraw %}



#### 5. **정렬 알고리즘 선택 가이드**


#### **데이터 크기 작고 간단한 정렬**: **삽입 정렬, 선택 정렬**

- **이유**: 삽입 정렬과 선택 정렬은 구현이 간단하고, 작은 데이터셋에서는 그리 효율이 떨어지지 않는다. 특히 데이터가 매우 작을 때는 O(n²) 시간 복잡도도 큰 문제가 되지 않아서, 간단한 구현과 이해를 위해 자주 사용된다.

#### **데이터가 거의 정렬되어 있을 때**: **삽입 정렬**

- **이유**: 삽입 정렬은 이미 거의 정렬된 데이터에 대해 매우 효율적으로 동작한다. 최선의 경우 시간 복잡도가 O(n)으로, 배열이 거의 정렬된 상태에서 빠르게 정렬을 마칠 수 있다. 삽입할 위치만 찾으면 되기 때문에, 이동하는 요소가 적어져 성능이 좋아진다.

#### **일반적인 대규모 데이터 정렬**: **병합 정렬, 퀵 정렬, 힙 정렬**

- **이유**:
	- **병합 정렬**은 항상 O(n log n)의 시간 복잡도를 보장하기 때문에, 최악의 경우에도 일정한 성능을 기대할 수 있어. 추가적인 메모리가 필요하지만, 안정 정렬이면서도 큰 데이터셋에 적합하다.
	- **퀵 정렬**은 평균적으로 O(n log n)의 성능을 보여, 특히 내부 요소들이 고르게 분포된 경우 효율적이다. 추가 메모리가 거의 필요하지 않고, 제자리 정렬이 가능하다. 다만, 최악의 경우 O(n²)까지 성능이 떨어질 수 있다.
	- **힙 정렬**은 최악의 경우에도 O(n log n)의 성능을 보이며, 제자리 정렬이 가능하다. 안정적이지 않지만, 추가 메모리를 거의 사용하지 않아 대규모 데이터 정렬에 적합하다.

#### **정렬이 안정적이어야 할 때**: **병합 정렬, Timsort**

- **이유**:
	- **병합 정렬**은 안정 정렬이므로, 같은 값의 요소들이 원래의 순서를 유지하면서 정렬된다. 이는 동일한 값을 가진 데이터가 있는 경우 중요한 특성이다.
	- **Timsort**는 실제 자바의 `Arrays.sort()`와 `Collections.sort()`에서 사용되는 알고리즘으로, 안정적이고 실제 데이터에서 매우 효율적이다. 병합 정렬과 삽입 정렬의 장점을 결합해 효율적이면서도 안정적인 정렬을 제공한다.

#### **추가 메모리가 제한적일 때**: **퀵 정렬, 힙 정렬**

- **이유**:
	- **퀵 정렬**은 제자리 정렬로, 추가적인 메모리 공간이 거의 필요하지 않는다. 평균적으로 매우 빠르게 동작하므로, 메모리가 제한적인 환경에서 유리하다.
	- **힙 정렬**도 제자리 정렬로, 추가 메모리 공간이 필요하지 않으며, 최악의 경우에도 일정한 성능을 보여. 안정적이지 않지만, 메모리 사용을 최소화하면서 대규모 데이터를 처리할 수 있다.
