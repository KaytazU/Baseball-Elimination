# Baseball-Elimination
A solution for the baseball elimination problem

Baseball elimination is a problem of deciding on which team does not have any chance of getting the most number of points or tieing for the most number of points given the standing of a sports league at any point of time during the season. Most games result in a set of possible assigned points rather than the scores obtained during the game. This system of point assignment can be defined as payoff pairs. For example, baseball has a payoff pair of (1,0), where winner gets 1 point and loser of the match gets 0 points. On the other hand, european football has the payoff pairs (3,0) and (1,1), where in case of a tie both teams get 1 point, winner of a match gets 3 points and loser gets 0 points. Although the problem can be defined as an optimization problem and solved using linear programming, elimination can also be decided based on a network flow approach.


Definition 1: Assume team x has won w[x] games and has g[x] games left to play and in total can win m[x]=w[x]+g[x] games at most.
Definition 2: Let g[x][y] be the number of games x will play with team y.
Definition 3: Let g be the number of points leader of the league has won until that point.
A naive approach would be to think that m[x] greater than or equal to g would be sufficient to say that x still has a chance to win the league. The reason for this not being sufficient but necessary is that losing games of the the leader will increase the points of other teams in the league in a given scenario during the rest of season.

Definition 4: g* =  g[p][q] for all p,q is the total number of games left in the league
Theorem 1: There is way for team x to tie or strictly win the league if and only if the flow value is equal to the g* 



Generalization of Problem Definition

Definition 5: A set of payoff pairs is called “monotonic” if it is possible to move to an another outcome which increases the points of one team, without increasing the points for the other team.

Definition 5 can be further explained by the following examples of payoff pairs. Baseball={(1,0)}, Hockey={(2,0),(1,1)}, Football={(3,0),(1,1)}. As we move in football or hockey from tie points (1,1) to another pair monotonicity condition holds. However, if an imaginative game would give (5,5) points to a tie and (3,0) points to a winner-loser situation then that game would not be monotonic.

Theorem 2: There is a number m* such that team i is eliminated if and only if m[i] is smaller than m*, if the game is monotonic

Theorem 2 states that there is universal number based on the whole set of teams that can be used to decide for elimination rather than solving the network for each team separately. 

Proof of  theorem 2: Let S be the a scenario for the remaining games, m(S) be the maximum number of points any team gets under scenario S. This means that m(S) is the best outcome that happens to any of the teams when we finish the season with scenario S.

Let m* be the supremum of all m(S), which means its the minimum m(S) over all scenarios. Let s* be the scenario where  m(s*) = m*. Note that finding s* requires looking at all scenarios, which is finite but inefficient procedure.

If m(i) is smaller that m* for a team then there is no scenario where team i has the most points ot tie for the most points. So team i is eliminated. On the other hand, suppose m(i) is greater than or equal to m* then there is a scenario where team i gets the most points or is tied for the most points.

If team i gets m* points in scenario s*, team i is not eliminated. If it does not get m* under scenario s* then in s* team i gets less than m(i) points. Therefore, we can go back to the future possible games for team i in that scenario and change the outcomes for team i to get  the maximum amount of points and reach m(i). In this case the points its opponents gets will either stay the same or decrease due to monotonicity. Let resulting scenario be s’ where team i wins m(i) greater than or equal to m* points and no other team wins more than m*. So s’ is becomes the scenario where i has the most points or ties for most points.


Complexity Analysis

At each iteration of Ford-Fulkerson algorithm depth-first search is performed. Complexity of depth first search is O(E) if we assume that E is number of edges.  Furthermore, number of edges has the complexity of number of teams to the power 2 due to the edges from each team pair. Assuming maximum number of flow iteration is f, we have have total time complexity of O(f*(number_of_teams^2)).




