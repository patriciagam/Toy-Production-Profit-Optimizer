# Toy Production Profit Optimizer

Integer linear programming solution (Python + PuLP) that computes the maximum daily profit of a toy factory selling both individual toys and special 3-toy bundles, subject to per-toy and total production limits.

Project 3 of Análise e Síntese de Algoritmos (Analysis and Synthesis of Algorithms), Instituto Superior Técnico, 2023/2024.

## The problem

UbiquityInc produces t different wooden toys. Each toy `i` has:
- a profit `l_i`
- a maximum daily production capacity `c_i`

The company can also sell p special packages, each made of three distinct toys, whose profit is higher than the sum of the individual toy profits. Total daily production is capped at max toys.

The goal is to find the maximum profit achievable per day.

## Model

Variables (all non-negative integers):
- toy_i: units of toy `i` sold individually (`toy_i <= c_i`)
- pack_k: units of package `k` produced

## Constraints:

For every toy i: `toy_i + sum of pack_k` over packages containing `i <= c_i`
Total production: `sum(toy_i) + 3 * sum(pack_k) <= max`

## Objective:

Maximize  `sum(l_i * toy_i) + sum(l_k * pack_k)`

The theoretical analysis gives O(t + p) variables and O(t + p) constraints. Experiments on 17 instances of increasing size show running time growing linearly with the size of the LP, in line with that analysis.

## Input format:
t p max  \
l_1 c_1  \
...  \
l_t c_t  \
i j k l_ijk        (p lines, one per package)  \
...  

## Example:

5 2 150  \
50 27  \
30 33  \
45 30  \
40 37  \
35 35  \
1 3 5 130  \
2 3 4 130  

Expected output: 6440
