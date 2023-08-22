# C Programming Language Course

## Variables

## Array

Mảng là một tập hợp tuần tự các phần tử có cùng kiểu dữ liệu và các phần tử được lưu trữ trong một dãy các ô nhớ liên tục trên bộ nhớ. Các phần tử của mảng được truy cập bằng cách sử dụng “chỉ số”.

### Mảng 1 chiều 

Mảng 1 chiều là một cấu trúc dữ liệu trong lập trình được sử dụng để lưu trữ một tập hợp các phần tử có cùng kiểu dữ liệu và được xếp theo thứ tự trong một dòng duy nhất. Các phần tử 

Ví dụ về khai báo mảng 1 chiều:
```c
int myArray[5]; 
```
Sau khi khai báo, chúng ta có thể gán giá trị cho từng phần tử của mảng thông qua chỉ số của nó:
```c
myArray[0] = 10; 
myArray[1] = 20;
// ...
```
Chúng ta cũng có thể truy xuất giá trị của các phần tử trong mảng bằng cách sử dụng chỉ số:
```c
int value = myArray[2];
```
Mảng được lưu trữ trong bộ nhớ máy tính theo cách liên tiếp và tuần tự. Khi một mảng được khai báo, hệ điều hành (hoặc trình biên dịch) sẽ cấp phát một phần của bộ nhớ liên tiếp để lưu trữ các phần tử của mảng. Mỗi phần tử trong mảng được lưu trữ tại một vị trí ô nhớ duy nhất.

Để truy cập một phần tử trong mảng, hệ thống sử dụng công thức tính địa chỉ ô nhớ của phần tử đó. Công thức này thường dựa trên kích thước của kiểu dữ liệu của mảng và chỉ số của phần tử. Ví dụ, để truy cập phần tử thứ i trong mảng, hệ thống có thể tính địa chỉ bằng công thức: địa chỉ_đầu_mảng + (kích_thước_phần_tử * i).

Ví dụ, giả sử chúng ta có một mảng kiểu số nguyên 4-byte (int) gồm 5 phần tử. Khi mảng này được khai báo, hệ điều hành sẽ cấp phát một vùng nhớ 20 byte (4 byte * 5 phần tử) liên tiếp cho mảng. Các phần tử sẽ được lưu trữ theo thứ tự từ địa chỉ đầu mảng.
```c
int myArray[5]; // Khai báo mảng gồm 5 phần tử kiểu int

&myArray[0] // địa chỉ đầu mảng 
&myArray[1] // địa chỉ đầu mảng + 4 byte (kích thước của kiểu int)
&myArray[2] // địa chỉ đầu mảng + 8 byte (kích thước của kiểu int * 2)
// ...
```
Các thao tác với mảng 1 chiều
- Nhập xuất phần tử trong mảng
- Tìm kiếm phần tử trong mảng
- Sắp xếp phần tử trong mảng
- Xóa phần tử trong mảng
```c
#include <stdio.h>

#define MAX_SIZE 100

void nhapMang(int arr[], int size) {
    int i;
    
    printf("Nhap cac phan tu trong mang:\n");
    for (i = 0; i < size; i++) {
        printf("arr[%d] = ", i);
        scanf("%d", &arr[i]);
    }
}

void xuatMang(int arr[], int size) {
    int i;
    
    printf("Cac phan tu trong mang:\n");
    for (i = 0; i < size; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

int timKiem(int arr[], int size, int key) {
    int i;
    
    for (i = 0; i < size; i++) {
        if (arr[i] == key) {
            return i; // Trả về chỉ số của phần tử nếu tìm thấy
        }
    }
    
    return -1; // Trả về -1 nếu không tìm thấy
}

void sapXep(int arr[], int size) {
    int i, j, temp;
    
    for (i = 0; i < size - 1; i++) {
        for (j = 0; j < size - i - 1; j++) {
            if (arr[j] > arr[j+1]) {
                // Hoán đổi giá trị của hai phần tử
                temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
            }
        }
    }
}

void xoaPhanTu(int arr[], int *size, int index) {
    int i;
    
    if (index < 0 || index >= *size) {
        printf("Khong the xoa phan tu\n");
        return;
    }
    
    for (i = index; i < *size - 1; i++) {
        arr[i] = arr[i+1];
    }
    
    (*size)--;
}

int main() {
    int myArray[MAX_SIZE];
    int n, i, key, found = 0;
    
    printf("Nhap so luong phan tu trong mang: ");
    scanf("%d", &n);
    
    nhapMang(myArray, n);
    
    printf("Cac phan tu trong mang:\n");
    xuatMang(myArray, n);
    
    printf("Nhap phan tu can tim kiem: ");
    scanf("%d", &key);
    
    int index = timKiem(myArray, n, key);
    if (index != -1) {
        printf("Tim thay phan tu %d tai vi tri %d\n", key, index);
    } else {
        printf("Khong tim thay phan tu %d trong mang\n", key);
    }
    
    sapXep(myArray, n);
    
    printf("Mang sau khi sap xep:\n");
    xuatMang(myArray, n);
    
    printf("Nhap vi tri phan tu can xoa: ");
    scanf("%d", &index);
    
    xoaPhanTu(myArray, &n, index);
    
    printf("Mang sau khi xoa phan tu:\n");
    xuatMang(myArray, n);
    
    return 0;
}
```
### Mảng nhiều chiều 
Mảng nhiều chiều là một cấu trúc dữ liệu trong lập trình được sử dụng để lưu trữ và quản lý các phần tử có cùng kiểu dữ liệu trong một hệ thống nhiều chiều.
Ví dụ khai báo mảng 2 chiều, gán giá trị và  truy xuất giá trị của các phần tử trong mảng
```c

int myArray[3][4]; // Khai báo mảng hai chiều gồm 3 hàng và 4 cột

myArray[0][0] = 10; // Gán giá trị 10 cho phần tử ở hàng 0, cột 0
myArray[1][2] = 20; // Gán giá trị 20 cho phần tử ở hàng 1, cột 2

int value = myArray[2][3]; // Lấy giá trị của phần tử ở hàng 2, cột 3
```

Mảng nhiều chiều được tổ chức dưới dạng các mảng một chiều lồng nhau. Mỗi chiều trong mảng nhiều chiều tương ứng với một mảng một chiều. Chúng ta có thể truy cập các phần tử trong mảng nhiều chiều bằng cách sử dụng các chỉ số tương ứng với từng chiều.

Mảng nhiều chiều được lưu trữ trong bộ nhớ máy tính theo cách tương tự như mảng một chiều, tuy nhiên có một số điểm khác biệt trong việc tính toán địa chỉ ô nhớ của các phần tử.

Khi một mảng nhiều chiều được khai báo, hệ điều hành (hoặc trình biên dịch) sẽ cấp phát một vùng nhớ liên tiếp để lưu trữ các phần tử của mảng. Mảng nhiều chiều được tổ chức dưới dạng các mảng một chiều lồng nhau, với các phần tử cấp cao được lưu trữ gần với địa chỉ bộ nhớ bắt đầu của mảng.

Ví dụ, giả sử chúng ta có một mảng hai chiều kiểu số nguyên 4-byte (int) gồm 3 hàng và 4 cột. Khi mảng này được khai báo, hệ điều hành sẽ cấp phát một vùng nhớ 48 byte (4 byte * 3 hàng * 4 cột) liên tiếp cho mảng. Các phần tử sẽ được lưu trữ theo thứ tự từ địa chỉ đầu mảng.

```c
int myArray[3][4]; // Mảng hai chiều gồm 3 hàng và 4 cột


&myArray[0][0] // địa chỉ đầu mảng
&myArray[0][1] // địa chỉ đầu mảng + 4 byte (kích thước của kiểu int)
&myArray[0][2] // địa chỉ đầu mảng + 8 byte (kích thước của kiểu int * 2)

&myArray[1][0] // địa chỉ đầu mảng + 16 byte (kích thước của kiểu int * 4)
&myArray[1][1] // địa chỉ đầu mảng + 20 byte (kích thước của kiểu int * 4 + 4 byte)

&myArray[2][3] // địa chỉ đầu mảng + 44 byte (kích thước của kiểu int * 8 + 12 byte)
```
Các thao tác với mảng 2 chiều
- Nhập xuất phần tử trong mảng
- Tìm kiếm phần tử trong mảng
- Sắp xếp phần tử trong mảng
- Xóa phần tử trong mảng
```c
#include <stdio.h>

// Hằng số định nghĩa kích thước mảng
#define ROWS 3
#define COLS 4

// Hàm nhập mảng
void inputArray(int arr[ROWS][COLS]) {
    printf("Nhập các phần tử của mảng:\n");
    for (int i = 0; i < ROWS; i++) {
        for (int j = 0; j < COLS; j++) {
            printf("arr[%d][%d] = ", i, j);
            scanf("%d", &arr[i][j]);
        }
    }
}

// Hàm xuất mảng
void outputArray(int arr[ROWS][COLS]) {
    printf("Các phần tử của mảng:\n");
    for (int i = 0; i < ROWS; i++) {
        for (int j = 0; j < COLS; j++) {
            printf("%d ", arr[i][j]);
        }
        printf("\n");
    }
}

// Hàm tìm kiếm phần tử trong mảng
void searchElement(int arr[ROWS][COLS], int target) {
    int found = 0; // Biến kiểm tra phần tử có tồn tại trong mảng hay không

    for (int i = 0; i < ROWS; i++) {
        for (int j = 0; j < COLS; j++) {
            if (arr[i][j] == target) {
                printf("Phần tử %d được tìm thấy tại vị trí arr[%d][%d]\n", target, i, j);
                found = 1;
            }
        }
    }
    if (!found) {
        printf("Không tìm thấy phần tử %d trong mảng\n", target);
    }
}

// Hàm sắp xếp mảng theo thứ tự tăng dần
void sortArray(int arr[ROWS][COLS]) {
    for (int k = 0; k < ROWS * COLS - 1; k++) {
        for (int i = 0; i < ROWS; i++) {
            for (int j = 0; j < COLS - 1; j++) {
                if (arr[i][j] > arr[i][j + 1]) {
                    // Hoán đổi giá trị của hai phần tử
                    int temp = arr[i][j];
                    arr[i][j] = arr[i][j + 1];
                    arr[i][j + 1] = temp;
                }
            }
        }
    }
}

// Hàm xóa phần tử khỏi mảng
void deleteElement(int arr[ROWS][COLS], int target) {
    int found = 0; // Biến kiểm tra phần tử có tồn tại trong mảng hay không

    for (int i = 0; i < ROWS; i++) {
        for (int j = 0; j < COLS; j++) {
            if (arr[i][j] == target) {
                arr[i][j] = 0; // Gán giá trị 0 cho phần tử cần xóa
                found = 1;
            }
        }
    }

    if (found) {
        printf("Đã xóa phần tử %d khỏi mảng\n", target);
    } else {
        printf("Không tìm thấy phần tử %dtrong mảng\n", target);
    }
}

int main() {
    int myArray[ROWS][COLS];

    inputArray(myArray);
    outputArray(myArray);

    int target;
    printf("Nhập phần tử cần tìm kiếm: ");
    scanf("%d", &target);
    searchElement(myArray, target);

    sortArray(myArray);
    printf("Mảng sau khi được sắp xếp:\n");
    outputArray(myArray);

    printf("Nhập phần tử cần xóa: ");
    scanf("%d", &target);
    deleteElement(myArray, target);
    printf("Mảng sau khi xóa phần tử:\n");
    outputArray(myArray);

    return 0;
}
```
## Decision

## Looping

## Function

## Macro

## Bit Operation

## Memory Management

## Pointer Basic 

## Pointer Advance

## Data Structure

## Algorithms

Thuật toán được chia ra nhiều loại khác nhau, tuy nhiên, note này chỉ nói đến thuật toán cơ bản là tìm kiếm và sắp xếp trên mảng hoặc trên danh sách liên kết.

### Searching algorithm

Mục đích của thuật toán tìm kiếm là tìm ra dữ liệu tương ứng với khóa $k$ trong danh sách. Dữ liệu tìm kiếm có thể là chỉ số của phần tử trong mảng hoặc dữ liệu được người dùng định nghĩa. Ví dụ:

```c
struct data {
    int key; // khóa tìm kiếm
    int data; // dữ liệu
};
```

Mỗi thuật toán lại có độ phức tạp tính toán khác nhau. Cần để ý đến:

- The average time.
- The worst-case time and.
- The best possible time.

#### Linear Search

Tìm kiếm tuần tự là phương pháp tìm kiếm phần tử trong một mảng hay một danh sách liên kết bằng cách so sánh lần lượt từng phần tử trong danh sách với khóa k.

Ví dụ tìm kiếm vị trí phần tử $k$ trong mảng:

```c
int find(int *arr, int len, int k) {
    for (int i = 0; i < len; i++) {
        if (arr[i] == k) {
            return i;
        }
    }
    return -1;
}
```

Ví dụ tìm kiếm phần tử $k$ trong danh sách liên kết:

```c
struct node {
    int key;
    int data;
    struct node* next;
};

struct node* find(struct node* node, int k) {
    struct node *inode;
    for (inode = node; inode->next != NULL; inode = inode->next) {
        if (inode->key == k) {
            return inode;
        }
    }
    return NULL;
}
```

Có thể thấy, với mỗi phần tử trong danh sách, có 2 thao tác so sánh được thực hiện: Kiểm tra điều kiện dừng khi hết mảng và kiểm tra phần tử hiện tại thỏa mãn hay chưa. Có thể tối ưu thao tác này bằng cách thay thế phần tử tìm kiếm cuối cùng bằng phần tử có khóa hợp lệ (**phần tử chặn**). Như vậy, chắc chắn sẽ tìm thấy phần tử trong mảng và không cần kiểm tra điều kiện hết mảng. Ví dụ minh họa:

```c
int find(int *arr, int len, int k) {
    int last = arr[len-1];
    arr[len-1] = k; // đặt phần tử cuối cùng = k

    int i;
    while (arr[i] != k) {
        i+=1;
    }
    
    arr[len-1] = last; // trả lại giá trị phần tử cuối

    if (i == len - 1) {
        if (last == k) {
            return len - 1;
        } else {
            return -1;
        }
    } else {
        return i;
    }
}
```

Độ phức tạp thời gian:

- Trường hợp xấu nhất: $O(n)$ khi phần tử tìm kiếm ở cuối cùng hoặc không có.
- Trường hợp tốt nhất: $O(1)$ khi phần tử tìm kiếm ở đầu danh sách.
- Trung bình: $O(\frac{n}{2}) = O(n)$ khi phần tử ở giữa danh sách.

#### Binary Search

Đối với danh sách kiểu mảng (**có thể truy cập phần tử bằng chỉ số**) đã được sắp xếp, việc tìm kiếm có thể được cải thiện đáng kể. Khi so sánh khóa $k$ với phần tử giữa danh sách, dựa vào kết quả so sánh mà **một nửa danh sách** có thể được loại bỏ do biết **chắc chắn** là các phần tử trong đó nhỏ hơn hoặc lớn hơn khóa tìm kiếm $k$.

Ví dụ tìm kiếm với $k = 8$ trong dãy $[1, 2, 3, 4, 5, 6, 7, 8, 9]$ có phần tử chính giữa bằng $5$. Với $k=8>5$, ta sẽ chỉ cần tìm kiếm $k$ trong dãy $[6, 7, 8, 9]$ với phương pháp tương tự.

```c
// tìm kiếm trong danh sách tăng dần
int binary_search(int *arr, int first, int last, int k) {
    if (last >= first) {
        int mid = (first+last)/2; // first + (last-first)/2
        if (arr[mid] == k) {
            return mid;
        } else if (arr[mid] > k) {
            // phần tử hiện tại lớn hơn khóa
            // -> tìm kiếm ở nửa trước
            binary_search(arr, first, mid-1, k);
        } else {
            // phần tử hiện tại nhỏ hơn khóa
            // -> tìm kiếm ở nửa sau
            binary_search(arr, mid+1, last, k);

        }
        
    } else {
        // last < first: danh sách rỗng - không tìm thấy
        return -1;
    }
}
```

Độ phức tạp thời gian:

- Trường hợp xấu nhất: $O(log(n))$
- Trường hợp tốt nhất: $O(1)$
- Trường hợp trung bình: $O(log(n))$

### Sorting algorithm

#### Insertion Sort

```c
void insertion_sort(int *arr, int n) {
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        for (j = i - 1; j>=0; j--) {
            if (arr[j] > key) {
                arr[j+1] = arr[j];
            } else {
                break;
            }
        }
        arr[j+1] = key;
    }
}
```

#### Bubble Sort

```c
void bubble_sort(int*arr, int n) {
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n-i-1; j++) {
            if(arr[j] > arr[j+1]) {
                int temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
            }
        }
    }
}
```

#### Selection Sort

```c
void selection_sort(int *arr, int n) {
    for (int i = 0; i < n-1; i++) {
        int index_min = i;
        int min = arr[i];
        
        // tìm chỉ số và giá trị phần tử nhỏ hơn arr[i]
        for (int j = i+1; j < n; j++) {
            if (arr[j] < min) {
                index_min = j;
                min = arr[j];
            }
        }
        arr[index_min] = arr[i];
        arr[i] = min;
    }
}
```

#### Quick Sort

```c

void swap(int* a, int* b)
{
    int t = *a;
    *a = *b;
    *b = t;
}

// Partition the array using the last element as the pivot
int partition_sort(int arr[], int low, int high)
{
    // Choosing the pivot
    int pivot = arr[high];
 
    // Index of smaller element and indicates
    // the right position of pivot found so far
    int i = (low - 1);
 
    for (int j = low; j <= high - 1; j++) {
 
        // If current element is smaller than the pivot
        if (arr[j] < pivot) {
 
            // Increment index of smaller element
            i++;
            swap(&arr[i], &arr[j]);
        }
    }
    swap(&arr[i + 1], &arr[high]);
    return (i + 1);
}
 
// The main function that implements QuickSort
// arr[] --> Array to be sorted,
// low --> Starting index,
// high --> Ending index
void quickSort(int arr[], int low, int high)
{
    if (low < high) {
 
        // pi is partitioning index, arr[p]
        // is now at right place
        int pi = partition_sort(arr, low, high);
 
        // Separately sort elements before
        // partition and after partition
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}
```

## Optimization

## Common Defects

## Unit Testing

## Git Version Control
