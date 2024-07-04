## The Kra Canal Optimization Problem

Located on the Malay Peninsula, the Kra Isthmus is a thin strech of land seperating the Indian Ocean and the Gulf of Thailand. Due to the large flow of trade between these two regions, there has been a historic interest in creating a canal through the isthmus to better faciliate maritime trade. Interest in this hypothetical canal has resurfeced in recent years, and this paper sets out to explore some ways this canal could impact both regional and global economies. Focusing specifically on the petroleum market due to its data availability, the following scripts and papers describe an econometric model used to predict optimal trade route assignments between countries.


## Methodology

Given a set of exporting countries $I$ and a set of importing countries $J$, the total global cost $Z$ of importing crude oil can be approximated by the minimization problem:

$$
\text{min} \quad Z = \sum_{i \in I} \sum_{j \in J} x_{ij} \cdot (c_{ij} + t_{ij}) \cdot p_{ij}
$$

with $x_{ij}$ representing the volume of oil assigned to a given route from country $i$ to country $j$. As the goal of this optimization is to minimize cost, three sources of cost have been included in the model. $c_{ij}$ is the simple transport cost, calculated by the trade route distance times the cost per distance of that transport method. Other non-transport costs are represented by $t_{ij}$, and the goal of this variable is to catch more abstract measures such as tariffs and free trade-agreements that may additionally affect import decisions. Finally, a variable $p_{ij}$ acts as a penalization factor for over-reliance on one specific country for imports according to the formula:

$$
p_{ij} = \left(1.01\right)^{\max\left(0, \frac{x_{ij}}{\sum_{i \in I} x_{ij}} - \alpha\right) \times 100} \quad \forall i \in I, j \in J
$$

In the real world, diversification of petroleum imports is often motivated by both national governments and private enterprises seeking to strike a balance between cutting costs while protecting energy security from volatile markets. Here, this diversification penalty occurs when trade from country $i$ to $j$ makes up more than $\alpha$ percent of country $j$'s oil imports, raising $p_{ij}$ by whatever amount this threshold has been passed by.

Restrictions in the model include production and demand capacities, with the sum of each country's imports and exports fixed at some values $D$ and $L$, respectively:

$$
\sum_{i \in I} x_{ij} = D_j \quad \forall  j \in J
$$

$$
\sum_{j \in J} x_{ij} = L_i \quad \forall i \in I
$$

Traded quantities and prices of all types are constrained to real non-negative numbers:

$$
x_{ij}, c_{ij}, p_{ij} \geq 0 \quad \forall i \in I, j \in J
$$

This optimization problem with variable vector $x_{ij}$ and parameters $c_{ij}$, $t_{ij}$, $p_{ij}$, and $\alpha$ computes in its double integral the total cost of all trade routes between all countries. As one can see, solving for the optimal trade routes in a hypothetical scenario requires the knowledge of quite a few parameters. Values of $c_{ij}$ can be estimated in a way that I will discuss in more detail in the next section, but the parameters of $t_{ij}$ $\alpha$ are less intuitive. As a result, the approach for applying this model to a set of trade routes modified by the construction of a canal can be summarized  by two steps:

1. Using current real-world trade route distances and trade volumes, infer the values of $p_{ij}$ and $\alpha$ that would result in the current trade volumes $x_{ij}$ being optimal by the objective function $Z$. 
  
2. Once solved for $p_{ij}$ and $\alpha$, modify transport costs $c_{ij}$ to reflect the construction of the Thai canal and solve again for $x_{ij}$
