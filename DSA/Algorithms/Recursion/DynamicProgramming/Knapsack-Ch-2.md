# Knapsack pattern

- ## Recursion:

  ### How to memoize?

  - https://www.youtube.com/watch?v=fJbIuhs24zQ&list=PL_z_8CaSLPWekqhdCPmFohncHwz8TY2Go&index=4

- ## Tabulation:

  - https://www.youtube.com/watch?v=PfkBS9qIMRE
  - https://www.youtube.com/watch?v=bUSaenttI24

# Problems with a similar pattern

- Subset sum
- Equal sum partition
- Count of subsets sum with a given sum
- Min subset sum difference
- Partitions with Given Difference
- Perfect sum: We need to consider "0" elements in the subsets as well if the target/sum is 0. We need to calculate from j=0 in that case.
- Target sum

### Note

In the recurrence relation for the dynamic programming, we use dp[i - 1][j] instead of dp[i][j] as we build the solution row by row, and each row depends on the previous row.
