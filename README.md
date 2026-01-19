# 0-1-knapsack
public class Classroom {

    public static int knapsackTab(int[] val, int[] wt, int W) {

        int n = val.length;

        // dp[i][j] = max value using first i items with capacity j
        int[][] dp = new int[n + 1][W + 1];

        // Initialization already 0 by default
        // dp[i][0] = 0  (0 capacity)
        // dp[0][j] = 0  (0 items)

        for (int i = 1; i < n + 1; i++) {
            for (int j = 1; j < W + 1; j++) {

                int v = val[i - 1];   // value of current item
                int w = wt[i - 1];    // weight of current item

                // valid case
                if (w <= j) {
                    int include = v + dp[i - 1][j - w];
                    int exclude = dp[i - 1][j];
                    dp[i][j] = Math.max(include, exclude);
                } 
                // not valid
                else {
                    dp[i][j] = dp[i - 1][j];
                }
            }
        }

        return dp[n][W];
    }

    public static void main(String[] args) {

        int[] val = {15, 14, 10, 45, 30};
        int[] wt  = {2, 5, 1, 3, 4};
        int W = 7;

        int ans = knapsackTab(val, wt, W);
        System.out.println("Maximum value in Knapsack = " + ans);
    }
}
