#include <iostream>
#include <vector>
#include <algorithm>

// Function to solve the knapsack problem
int knapsack(const std::vector<int>& weights, const std::vector<int>& values, int capacity) {
    int n = weights.size();
    // Create a 2D DP array initialized to 0
    std::vector<std::vector<int>> dp(n + 1, std::vector<int>(capacity + 1, 0));

    // Build the dp array from the bottom up
    for (int i = 1; i <= n; ++i) {
        for (int w = 1; w <= capacity; ++w) {
            if (weights[i - 1] <= w) {
                // If the item can be included, decide to include it or not
                dp[i][w] = std::max(dp[i - 1][w], dp[i - 1][w - weights[i - 1]] + values[i - 1]);
            } else {
                // If the item cannot be included, carry forward the value
                dp[i][w] = dp[i - 1][w];
            }
        }
    }

    // The bottom-right cell contains the maximum value
    return dp[n][capacity];
}

int main() {
    // Example usage
    std::vector<int> weights = {1, 2, 3};
    std::vector<int> values = {10, 20, 30};
    int capacity = 5;

    int max_value = knapsack(weights, values, capacity);
    std::cout << "Maximum value in knapsack of capacity " << capacity << ": " << max_value << std::endl;

    return 0;
}
