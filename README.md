# ExpressionTargetCalculator

In a faraway land, a mathematician named Naina possesses a mystical array of numbers called "nums." Her challenge is to create a magical expression that results in a specific target number. Naina can concatenate the numbers in the array, and before each number, she must either place a "+" or a "-" to construct an expression.
Your task is to help Naina determine how many different ways she can form such expressions that will evaluate to the given target number. Can you figure out how many possible expressions will lead to the desired result?
Input
The first line of the input contains the integer N, denoting the number of elements in the array.
The second line of the input contains N space-separated integers, denoting the elements of the array nums.
The third line of the input contains a single integer T, denoting the target integer.

Constraints
1 ≤ N ≤ 20
0 ≤ nums[i] ≤ 1000
0 ≤ sum(nums[i]) ≤ 1000
-1000 ≤ T ≤ 1000

def find_ways(nums, index, current_sum, target, memo):
    if index == len(nums):
        return 1 if current_sum == target else 0
    
    if (index, current_sum) in memo:
        return memo[(index, current_sum)]
    
    add_ways = find_ways(nums, index + 1, current_sum + nums[index], target, memo)
    subtract_ways = find_ways(nums, index + 1, current_sum - nums[index], target, memo)
    
    memo[(index, current_sum)] = add_ways + subtract_ways
    return memo[(index, current_sum)]

def count_expressions(nums, target):
    memo = {}
    return find_ways(nums, 0, 0, target, memo)

N = int(input())
nums = list(map(int, input().split()))
T = int(input())

print(count_expressions(nums, T))
