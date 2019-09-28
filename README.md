# mlrose: Machine Learning, Randomized Optimization and SEarch
mlrose is a Python package for applying some of the most common randomized optimization and search algorithms to a range of different optimization problems, over both discrete- and continuous-valued parameter spaces.

## Key Differences in this Fork
- Added OnePointCrossOver
	- Crossover method can be selected manually with DiscreteOpt crossover parameter of "OnePoint" or "Uniform" (default).
- Modified semantics of "attempts", "iterations", and "restarts" for the following algorithms:
	- random_hill_climb
		- The original code treated "restarts" as forced repetitions of the entire algorithm.
		- My change ignores the "restarts" parameter and allows the algorithm to restart on its own as it gets stuck at an optima.
		- Within each iteration, "max_attempts" is used to determine how many times to test a random neighbor for betterness before giving up and restarting.
		- The algorithm will run for the exact number of iterations specified by "max_iters".
	- simulated_annealing
		- My code removes the usage of "max_attempts".
		- Each random neighbor selection (and possible movement to it) is considered a single iteration.
		- The algorithm will run for the exact number of iterations specified by "max_iters".
	- genetic_alg
		- The original code would try up to "max_attempts" different generated populations per iteration in hopes of finding a better one.
		- My code removes the usage of "max_attempts".
		- Each generation is considered a single iteration, regardless of whether it is better than the previous.
		- The algorithm will run for the exact number of iterations specified by "max_iters".
	- mimic
		- The original code would try up to "max_attempts" different sample populations per iteration in hopes of finding a better one.
		- My code removes the usage of "max_attempts".
		- The generation of a new sample population is considered a single iteration, regardless of whether it is better than the previous.
		- The algorithm will run for the exact number of iterations specified by "max_iters".
- Misc Notes
	- There is still potentially a lot of code referencing some of the disregarded variables.
	- There is no guarantee that the "generators" and "runners" will continue to function as intended. I haven't used or tested them.


## Project Background
mlrose was initially developed to support students of Georgia Tech's OMSCS/OMSA offering of CS 7641: Machine Learning.

It includes implementations of all randomized optimization algorithms taught in this course, as well as functionality to apply these algorithms to integer-string optimization problems, such as N-Queens and the Knapsack problem; continuous-valued optimization problems, such as the neural network weight problem; and tour optimization problems, such as the Travelling Salesperson problem. It also has the flexibility to solve user-defined optimization problems. 

At the time of development, there did not exist a single Python package that collected all of this functionality together in the one location.

## Main Features

#### *Randomized Optimization Algorithms*
- Implementations of: hill climbing, randomized hill climbing, simulated annealing, genetic algorithm and (discrete) MIMIC;
- Solve both maximization and minimization problems;
- Define the algorithm's initial state or start from a random state;
- Define your own simulated annealing decay schedule or use one of three pre-defined, customizable decay schedules: geometric decay, arithmetic decay or exponential decay.

#### *Problem Types*
- Solve discrete-value (bit-string and integer-string), continuous-value and tour optimization (travelling salesperson) problems;
- Define your own fitness function for optimization or use a pre-defined function.
- Pre-defined fitness functions exist for solving the: One Max, Flip Flop, Four Peaks, Six Peaks, Continuous Peaks, Knapsack, Travelling Salesperson, N-Queens and Max-K Color optimization problems.

#### *Machine Learning Weight Optimization*
- Optimize the weights of neural networks, linear regression models and logistic regression models using randomized hill climbing, simulated annealing, the genetic algorithm or gradient descent;
- Supports classification and regression neural networks.

## Installation
mlrose was written in Python 3 and requires NumPy, SciPy and Scikit-Learn (sklearn).

The latest released version is available at the [Python package index](https://pypi.org/project/mlrose/) and can be installed using `pip`:
```
pip install mlrose
```

## Documentation
The official mlrose documentation can be found [here](https://mlrose.readthedocs.io/). 

A Jupyter notebook containing the examples used in the documentation is also available [here](https://github.com/gkhayes/mlrose/blob/master/tutorial_examples.ipynb).

## Licensing, Authors, Acknowledgements
mlrose was written by Genevieve Hayes and is distributed under the [3-Clause BSD license](https://github.com/gkhayes/mlrose/blob/master/LICENSE). 

You can cite mlrose in research publications and reports as follows:
* Hayes, G. (2019). ***mlrose: Machine Learning, Randomized Optimization and SEarch package for Python***. https://github.com/gkhayes/mlrose. Accessed: *day month year*.

BibTeX entry:
```
@misc{Hayes19,
 author = {Hayes, G},
 title 	= {{mlrose: Machine Learning, Randomized Optimization and SEarch package for Python}},
 year 	= 2019,
 howpublished = {\url{https://github.com/gkhayes/mlrose}},
 note 	= {Accessed: day month year}
}
```
