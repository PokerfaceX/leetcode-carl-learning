### Question 88 Merge Sorted Array

![image-20220902193836350](C:\Users\jason\AppData\Roaming\Typora\typora-user-images\image-20220902193836350.png)

这也是一道经典的双指针题目，其实思路并不复杂，分别用两个指针从头开始便利两个数组，哪个数值小，便把哪个数值放到最终的数组里面，如果数值一样的话可以随便放一个，因为每次被放进去的都会是更小的数值，不会影响结果

~~~java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int[] array = new int[m + n];
        int i = 0, j = 0, k = 0;
        while (i < m && j < n) {
            if (nums1[i] < nums2[j]) {
                array[k] = nums1[i++];
            } else {
                array[k] = nums2[j++];
            }
            k++;
        }
        while (i < m) {
            array[k++] = nums1[i++];
        }
        while (j < n) {
            array[k++] = nums2[j++];
        }
        for(i = 0; i < m + n; i++) nums1[i] = array[i];
        
    }
}
~~~

