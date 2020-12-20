```java
class Solution {
    public int[] sortTransformedArray(int[] nums, int a, int b, int c) {
        if (nums.length == 0) return new int[]{};
        int n = nums.length;
        int[] res = new int[n];
        boolean rev = false;
        if (a == 0) {
            for (int i = 0; i < n; i++) res[i] = b * nums[i] + c;
            if (b < 0) rev = true;
        } else {
            if (a < 0) {
                rev = true;
            }
            double mid = 0.0 - (double) b / (double) (a * 2);
            Double diff = Double.MAX_VALUE;
            int start = 0;
            for (int i = 0; i < n; i++) {
                if (Math.abs(nums[i] - mid) < diff) {
                    start = i;
                    diff = Math.abs(nums[i] - mid);
                }
            }
            int p1 = start, p2 = start + 1, pos = 0;
            while (p1 >=0 && p2 < n) {
                if (mid - nums[p1] <= nums[p2] - mid) {
                    res[pos++] = calc(nums[p1--], a, b, c);
                } else {
                    res[pos++] = calc(nums[p2++], a, b, c);
                }
            }
            while (p1 >= 0) res[pos++] = calc(nums[p1--], a, b, c);
            while (p2 < n) res[pos++] = calc(nums[p2++], a, b, c);
        }
        if (rev) {
            for(int i = 0; i < n / 2; i++)
                {
                    int temp = res[i];
                    res[i] = res[n - i - 1];
                    res[n - i - 1] = temp;
                }
        }
        return res;
    }
    private int calc(int x ,int a, int b, int c) {
        return a * x * x + b * x + c;
    }
    
}
```

