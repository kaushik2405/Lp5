#include <iostream>
#include <vector>
#include <omp.h>
void parallelBubbleSort(std::vector<int>& arr) {
 int n = arr.size();
 bool swapped;
 #pragma omp parallel
 {
 do {
 swapped = false;
 #pragma omp for
 for (int i = 0; i < n - 1; i++) {
 if (arr[i] > arr[i + 1]) {
 std::swap(arr[i], arr[i + 1]);
 swapped = true;
 }
 }
 } while (swapped);
 }
}
int main() {
 std::vector<int> numbers = {5, 2, 8, 12, 3};
 std::cout << "Before sorting: ";
 for (int num : numbers) {
 std::cout << num << " ";
 }
 std::cout << std::endl;
 parallelBubbleSort(numbers);
 std::cout << "After sorting: ";
 for (int num : numbers) {
 std::cout << num << " ";
 }
 std::cout << std::endl;
 return 0;
}