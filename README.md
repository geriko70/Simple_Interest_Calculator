Simple & Compound Interest Calculator (Shell Script)

This is a basic, menu-driven shell script designed for quick financial calculations. It allows users to calculate either Simple Interest (SI) or Compound Interest (CI) using input parameters.

Features

Simple Interest Calculation (Option 1): Calculates simple interest based on Principal (P), Time (T), and Rate (R).

Compound Interest Calculation (Option 2): Calculates compound interest based on Principal (P), Time (T), Rate (R), and the number of times the interest is applied per year (n).

Menu Interface: Easy-to-use numbered menu for selection.

Floating-Point Precision: Uses the bc (basic calculator) utility for accurate floating-point arithmetic up to two decimal places.

Prerequisites

This script is written in Bash and requires the following utilities to be installed on your system:

bc (Basic Calculator): Essential for performing non-integer arithmetic (floating-point division and powers). Most Linux and macOS distributions have this installed by default.

# Check if bc is installed
which bc


Installation and Setup

Save the Script: Save the provided script content into a file named interest_calculator.sh.

#!/bin/bash

while [ 1 ]
do
echo "MENU"
echo "1. Simple Interest"
echo "2. Compound Interest"
echo "3. Exit"
echo "Enter Your Choice"
read choice
case $choice in
1) echo "Enter the values: Principal Amount,Time (In Years) and Rate of Interest"
read p
read t
read r
si=`echo "scale=2;( $p * $t * $r ) / 100" | bc`
echo "Simple Interest = $si" ;;
2) echo "Enter the values: Principal Amount,Time (In Years),Rate of Interest and
number of times interest applied per year"
read p
read t
read r
read n
power=`expr $n \* $t`
ci=`echo "scale=2; $p * ( 1 + $r / $n ) ^ $power" | bc`
echo "Compound Interest = $ci" ;;
3) exit;;
*) echo "Invalid Choice";;
esac
done


Make it Executable: Grant execution permissions to the script file.

chmod +x interest_calculator.sh


How to Run

Execute the script directly from your terminal:

./interest_calculator.sh


Usage Examples

1. Simple Interest (SI)

The formula used is: $$ SI = (P \times T \times R) / 100 $$

Input Sequence: Principal (P), Time in years (T), Rate of Interest (R).

Example: Calculate SI for a principal of 1000, time of 2 years, and rate of 5%.

Enter 1 for Simple Interest.

Enter 1000 (P)

Enter 2 (T)

Enter 5 (R)

Output: Simple Interest = 100.00

2. Compound Interest (CI)

The formula used to calculate the interest (not the total amount) is derived from:
$$ CI = A - P $$
where $A = P (1 + \frac{R}{n})^{nt}$ is the total Future Value (Amount). The script directly calculates $A$ and displays it as "Compound Interest" in the output (a slight misnomer in the script, as it calculates the Amount (A), not just the interest).

Input Sequence: Principal (P), Time in years (T), Annual Interest Rate (R), Number of times interest applied per year (n).

Example: Calculate CI (Amount A) for a principal of 1000, time of 1 year, rate of 10% (0.10), compounded annually (n=1).

Enter 2 for Compound Interest.

Enter 1000 (P)

Enter 1 (T)

Enter 0.10 (R - Note: Enter R as a decimal for this formula)

Enter 1 (n)

Output: Compound Interest = 1100.00 (This is the Total Amount $A$).

3. Exit

Enter 3 to exit the script gracefully.

Script Details

The script leverages the bc utility to handle mathematical operations involving fractions and exponents, which are not natively supported by standard shell arithmetic (expr or $(())).

scale=2: Sets the decimal precision for the calculation to two places.

The ^ operator is used within bc for exponentiation, necessary for the Compound Interest formula.
