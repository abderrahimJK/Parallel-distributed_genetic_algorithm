# Parallel-distributed_genetic_algorithm

This project demonstrates the use of a distributed genetic algorithm (GA) with an island model. 
The island model is a parallel GA approach where multiple subpopulations (islands) evolve independently and occasionally exchange individuals (migration) to improve the overall search process. 
The project is implemented using the JADE (Java Agent DEvelopment Framework) platform, which allows for easy communication between agents representing the islands.

## Problem Description

The problem we are solving in this project is to evolve a population of strings to match a target string. Each island (agent) maintains its own subpopulation and evolves it using genetic operators such as selection, crossover, and mutation. Periodically, the islands exchange their best individuals to promote diversity and improve the overall search process.

## Project Structure

### The project consists of two main classes:

`GeneticAlgorithm`: This class implements the genetic algorithm, including initialization, selection, crossover, and mutation. It also provides methods for adding individuals to the population and retrieving the best individual.

`GAIslandAgent`: This class extends the JADE Agent class and represents an island in the island model. It uses a TickerBehaviour to periodically run the genetic algorithm and a CyclicBehaviour to receive messages from other agents. The agent sends its best individual to other agents when the shouldExchangeBestIndividuals() method returns true.

`MasterAgent` This class is a JADE agent responsible for receiving and processing messages from other agents in the distributed genetic algorithm (GA) system. It extends the **Agent** class from the JADE framework and overrides the **setup()** method to define its behavior.

#### Class Structure

The `MasterAgent` class contains the following fields:

-⚜️ **sequentialBehaviour**: A SequentialBehaviour object that allows the agent to execute a sequence of behaviors.

-⚜️ **dfAgentDescription**: A DFAgentDescription object that describes the agent's properties in the Directory Facilitator (DF) service.

-⚜️ **serviceDescription**: A ServiceDescription object that describes the services provided by the agent.

#### Agent Behavior

The `setup()` method initializes the agent's behavior and registers its services with the Directory Facilitator (DF) service. The agent's behavior is defined using a CyclicBehaviour object, which is added to the sequentialBehaviour field.

The `CyclicBehaviour` object contains an `action()` method that is executed repeatedly. In this method, the agent receives messages from other agents and processes them as follows:

1 - If a message is received, the agent extracts its content and splits it into an array of strings using the `-` delimiter. The content is expected to be in the format `agentName-bestIndividual-fitness`.

2 - The agent prints the received information to the console, displaying the sender agent's name, the best individual, and its fitness.

3 - If the content of the message is equal to the target string "Hello SDIA", the agent sends a reply message with the content "done" to the sender agent.

4 - If no message is received, the agent blocks its execution until a new message arrives.

Finally, the `sequentialBehaviour` object is added to the agent using the `addBehaviour()` method, which starts the execution of the agent's behavior.

### methods

- `shouldExchangeBestIndividuals()` method in the GAIslandAgent class to determine when the agents should exchange their best individuals. 
- `sendBestIndividual()` method sends the best individual to other agents, and you can customize the list of agents by modifying the getOtherAgents() method.

#### Fitness Calculation
The `fitness(String candidate)` method calculates the fitness of a given candidate string. The fitness is determined by comparing each character of the candidate string with the corresponding character of the target string. If the characters at the same position are different, the fitness score is incremented by 1. The fitness score represents the total number of character mismatches between the candidate and the target string. `A lower fitness score indicates a better match to the target string.`

#### Best Individual Selection
The `getBestIndividual()` method selects the best individual from the population using `tournament selection`. Tournament selection is a method of selecting individuals based on their fitness by organizing a "tournament" among a few randomly chosen individuals from the population.

In this implementation, the tournament size is set to 5. 
The method initializes the `best` variable to store the best individual found so far and the `bestFitness` variable to store the fitness of the best individual. The `bestFitness` is initially set to `Integer.MAX_VALUE` to ensure that any candidate's fitness will be better than the initial value.

The method then iterates through the tournament size (5 in this case) and performs the following steps:

- Randomly select a candidate from the population.
- Calculate the fitness of the selected candidate using the `fitness(String candidate)` method.
- If the candidate's fitness is better (lower) than the current `bestFitness`, update the `best` variable with the candidate and the `bestFitness` variable with the candidate's fitness.

After the loop, the `best` variable contains the best individual found in the tournament, and the method returns it.

## Customization

You can customize the genetic algorithm by modifying the parameters in the GAIslandAgent class:

- `populationSize`: The size of the subpopulation maintained by each island.
- `stringLength`: The length of the strings in the population.
- `target`: The target string that the algorithm tries to evolve.
- `mutationRate`: The probability of mutation for each gene in an individual.


