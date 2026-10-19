# Artificial Intelligence - Chapter 8: Adversarial Search

## Lecture Note Slides (20 Slides)

**Source Materials:** AI - Chapter 8 (textbook); AI Lecture Notes 12 (AI and Game Playing)

---

## Slide 1 - Adversarial Search

**Adversarial Search: Games, Minimax, Alpha-Beta Pruning, and Beyond**

Chapter 8 - Adversarial Search

A scholarly treatment of decision-making in competitive environments where an intelligent opponent acts to minimize the agent's success.

---

## Slide 2 - Games as Adversarial Search Problems

Games are adversarial search problems: the agent (MAX) chooses moves to maximize its outcome, while an opponent (MIN) chooses moves to minimize the agent's outcome. Both act alternately, and each has perfect information about the state (in deterministic perfect-information games).

Why games are valuable AI research domains (Text Note 12):

- **Clear objectives:** Winning, losing, or drawing are well-defined
- **Measurable results:** Scores and outcomes make success easy to quantify
- **Training opportunities:** AI can learn from expert games, self-play, or repeated attempts
- **Self-play:** An agent can play against itself to generate training data
- **Performance comparisons:** AI can be compared against expert human players

Game-playing milestones (Text Note 12):

- 1997: Deep Blue defeated world chess champion Garry Kasparov
- 2016-2017: AlphaGo defeated Lee Sedol and Ke Jie at Go
- 2018: OpenAI Five competed against professional Dota 2 players
- 2019: AlphaStar reached Grandmaster level in StarCraft II

---

## Slide 3 - Games as Search Trees

A game is represented as a search tree:

- **State:** The current board configuration and whose turn it is
- **Action:** A legal move from the current state
- **Branch:** A transition from one state to another via an action
- **Node:** A particular state in the tree
- **Terminal state:** A state where the game ends (win, loss, or draw)

Example: Tic-tac-toe

- The AI (X) examines the board, identifies legal moves, considers opponent responses (O), and evaluates outcomes
- The tree branches at each move and continues until terminal states

Text Note 12 illustrates this with a tic-tac-toe tree showing AI moves branching to opponent responses.

---

## Slide 4 - Reward Values and Game Outcomes

Computers compare outcomes numerically. A simple scoring system:

- +1: Win for the AI
- 0: Draw
- -1: Loss for the AI

More sophisticated evaluation functions may assign continuous values (e.g., +0.7 for a slightly advantageous position) rather than only win/draw/loss.

Key distinction (Text Note 12):

- A **reward** is a numerical signal evaluating an outcome
- A **value estimate** predicts how beneficial a state or action is expected to be

The AI seeks actions leading to high-value states, accounting for the opponent's efforts to minimize that value.

---

## Slide 5 - The Minimax Algorithm

Minimax is a decision algorithm for two-player, turn-based, zero-sum games. It assumes both players play optimally:

- MAX (the AI) chooses actions to maximize its outcome
- MIN (the opponent) chooses actions to minimize MAX's outcome

Minimax works recursively:

1. Generate possible moves from the current state
2. Recursively explore future states to terminal nodes or a depth limit
3. Evaluate terminal states with the reward function; use a heuristic evaluation function for nonterminal states at the depth limit
4. Back up values: at MAX nodes, take the maximum of child values; at MIN nodes, take the minimum
5. Select the root action leading to the highest backed-up value

The algorithm assumes the opponent will always make the move worst for MAX - a pessimistic but sound assumption in zero-sum play.

---

## Slide 6 - Minimax Example

Suppose MAX has two moves, A and B:

Move A leads to two MIN responses:

- MIN response 1 → score +1
- MIN response 2 → score 0

Move B leads to two MIN responses:

- MIN response 1 → score -1
- MIN response 2 → score 0

Assuming MIN chooses the response least favorable to MAX:

- Move A's worst case = min(+1, 0) = 0
- Move B's worst case = min(-1, 0) = -1

MAX chooses Move A because its worst-case value (0) exceeds Move B's worst-case value (-1).

Key idea: MAX should not choose the move with the best possible outcome; it should choose the move with the best worst-case outcome against an optimal opponent.

---

## Slide 7 - Properties of Minimax

- **Optimal:** If both players play optimally and the tree is searched to termination, minimax determines the optimal move
- **Complete:** Yes - the search terminates at terminal states
- **Time complexity:** O(b^m) where b is the branching factor and m is the depth (number of plies)
- **Space complexity:** O(bm) - depth-first traversal stores only the path

Minimax is optimal but impractical for complex games due to combinatorial explosion:

- Checkers: ~10^20 states
- Chess: ~10^50 states
- Go: ~10^170 states
- (Approximate estimates; atoms in the observable universe ~10^80)

Exhaustive search is feasible only for small games like tic-tac-toe.

---

## Slide 8 - Tic-Tac-Toe: A Solved Game

Tic-tac-toe has a small enough state space for exhaustive minimax search.

Properties of optimal tic-tac-toe play:

- The AI wins when the opponent makes a mistake
- The AI forces a draw against optimal play
- The AI never loses from a valid starting position

**Solved game:** A game for which the optimal outcome from the initial position is known. For tic-tac-toe, perfect play by both sides yields a draw.

Important: Optimal play does not guarantee a win. Against an optimal opponent, the best achievable outcome in some games is a draw.

---

## Slide 9 - Alpha-Beta Pruning

Alpha-beta pruning is an optimization of minimax that eliminates branches that cannot affect the final decision, without changing the result.

It maintains two values at each node:

- **α (alpha):** The best (highest) value MAX has found so far along the path
- **β (beta):** The best (lowest) value MIN has found so far along the path

Pruning rules:

- At a MIN node: if a child's value ≤ α, prune remaining children (MAX already has a better option elsewhere)
- At a MAX node: if a child's value ≥ β, prune remaining children (MIN already has a better option elsewhere)

Alpha-beta pruning does not change the minimax value at the root; it only avoids computing values of irrelevant subtrees.

---

## Slide 10 - Alpha-Beta Effectiveness

Alpha-beta pruning's power depends on move ordering:

- **Ideal ordering** (best moves first): reduces effective branching factor to roughly b^(m/2), doubling search depth for the same computation
- **Worst ordering:** no pruning; equivalent to minimax

In practice, with reasonable move ordering (capture moves, killer heuristics, history heuristics), alpha-beta achieves near the ideal reduction.

For chess, alpha-beta with good move ordering makes deep search practical - a key factor in Deep Blue's success.

---

## Slide 11 - Heuristic Evaluation and Cutoff Search

For complex games, complete search to terminal states is impossible. Instead, search to a fixed depth d and apply a **heuristic evaluation function** to nonterminal leaf nodes:

The evaluation function estimates how favorable a position is for MAX:

- Positive values favor MAX
- Negative values favor MIN
- Zero is even

Examples:

- Chess: material count (pawn=1, knight=3, bishop=3, rook=5, queen=9) plus positional factors
- Go: territory and influence estimates

**Cutoff search:** minimax or alpha-beta with depth limit d and heuristic evaluation at frontier nodes.

Trade-off: deeper search improves accuracy but increases computation exponentially; shallower search is faster but less accurate.

---

## Slide 12 - Forward Pruning and Selective Search

Beyond alpha-beta, additional pruning methods reduce search:

**Forward pruning:** Skip entire branches without evaluating them, based on the assumption they cannot be good. Risky: may prune the optimal move.

Examples:

- **ProbCut:** uses statistical bounds to prune likely-unpromising branches
- **Null move pruning:** assumes the opponent passing cannot hurt them; if the position remains strong, prune

**Selective extensions:** Search deeper in forcing lines (captures, checks) where tactical precision matters.

Modern engines combine alpha-beta with forward pruning, selective extensions, and transposition tables (caching evaluated positions).

---

## Slide 13 - Monte Carlo Tree Search (MCTS)

For games with huge branching factors (Go) or where evaluation functions are hard to design, MCTS offers an alternative to minimax.

MCTS uses repeated simulations instead of exhaustive exploration. Each iteration has four phases:

1. **Selection:** Traverse the tree from root using a selection policy (e.g., UCT) balancing exploration and exploitation
2. **Expansion:** Add one or more new child nodes to a partially expanded node
3. **Simulation:** Play out the game from the new node using random or policy-guided moves to a terminal state
4. **Backpropagation:** Update node statistics (visit counts, win rates) along the path with the simulation result

After many iterations, choose the root child with the best statistics.

MCTS does not require an evaluation function - it learns from simulation outcomes. It is the foundation of AlphaGo's search component.

Text Note 12 describes MCTS as focusing computational effort on promising parts of the game tree without examining every state.

---

## Slide 14 - Combining Neural Networks with Search (AlphaGo)

AlphaGo (Text Note 12) combined two key ideas:

1. **Neural networks** estimate move quality (policy network) and position strength (value network)
2. **Monte Carlo Tree Search** examines promising futures using these estimates

The policy network suggests which moves are promising (reducing branching). The value network estimates who is winning from a position (reducing depth). MCTS uses both to focus search.

This hybrid approach:

- Uses learning to recognize patterns (position evaluation)
- Uses search to examine consequences (tactical lookahead)
- Achieved superhuman Go performance (2016-2017)

Text Note 12 notes this shows how different AI techniques work together rather than as separate approaches.

---

## Slide 15 - Games with Chance and Imperfect Information

Not all games fit minimax cleanly:

**Stochastic games (chance):** Backgammon, dice games, card draws. Expected minimax extends minimax by averaging over chance outcomes:

- Chance nodes take the expected value over possible dice rolls/card draws
- Compute expected value: Σ P(outcome) × value(outcome)

**Imperfect-information games:** Poker, bridge, card games with hidden hands. Players don't know the full state. Minimax assumes perfect information and doesn't directly apply.

Approaches for imperfect information:

- **Information sets:** Group states the player cannot distinguish
- **Counterfactual regret minimization (CFR):** Used in poker AI
- **Monte Carlo methods:** Sample possible hidden states

AI has achieved major success in poker (Text Note 12), showing uncertainty and bluffing do not automatically favor humans.

---

## Slide 16 - Real-Time Games and Time Constraints

Real-time strategy games (StarCraft II - Text Note 12) require decisions under time pressure while the game continues. Exhaustive search is impossible.

Approaches:

- **Learned policies:** Neural networks map state to action quickly
- **Limited-depth search:** Search as deep as time permits
- **Hierarchical planning:** Strategic (long-term) + tactical (short-term) decisions

Real-time games test an AI's ability to make effective decisions under constraints: time limits, uncertainty, and changing conditions (Text Note 12).

---

## Slide 17 - Adversarial Search and Agent Design

Adversarial search fits the utility-based agent model (Chapter 2): the agent's utility is +1 for a win, 0 for a draw, -1 for a loss, and it acts to maximize expected utility against an opponent minimizing it. The game tree is the agent's model of the environment, and minimax is the deliberation procedure.

However, adversarial search assumes a perfect-information, zero-sum, turn-based setting. Many real competitive scenarios are imperfect-information (poker), non-zero-sum (negotiation), or simultaneous-move (rock-paper-scissors, auctions). Extending beyond minimax to these settings requires game-theoretic solution concepts such as Nash equilibrium and counterfactual regret minimization, which are active research areas at the intersection of AI and economics.

---

## Slide 18 - Case Study: AlphaZero and Self-Play

AlphaZero extended AlphaGo's approach by learning entirely from self-play, without human game data. Starting from random play, it repeatedly:

1. Plays games against itself using MCTS guided by its current neural network
2. Records the resulting positions and outcomes
3. Trains its network to predict MCTS-improved move probabilities and game outcomes
4. Iterates, producing a stronger network and stronger MCTS

Within days, AlphaZero surpassed all prior Go, chess, and shogi programs. This demonstrates that search (MCTS) and learning (neural networks) form a powerful feedback loop: search generates better training data, and the network guides search more effectively. It is one of the clearest examples of learning + search combining to produce superhuman performance.

---

## Slide 19 - Summary: Key Takeaways

1. Games are adversarial search problems: MAX maximizes, MIN minimizes, in alternating turns
2. Game states form a search tree; terminal states receive win/draw/loss values
3. Minimax assumes optimal opponents and computes the best worst-case move; it is optimal but exponential O(b^m)
4. Alpha-beta pruning eliminates provably irrelevant branches without changing the minimax result; move ordering determines effectiveness
5. For complex games, cutoff search uses heuristic evaluation functions at depth-limited frontier nodes
6. Tic-tac-toe is solvable by exhaustive minimax; chess, Go, and larger games are not
7. Forward pruning and selective extensions further reduce search at some risk
8. Monte Carlo Tree Search uses simulations and statistics instead of exhaustive search; effective for Go and games without good evaluation functions
9. AlphaGo combined neural network evaluation with MCTS to achieve superhuman play
10. Stochastic games use expected minimax; imperfect-information games require information sets and methods like CFR

---

## Slide 20 - Review Questions

1. What makes a game an adversarial search problem, and how do MAX and MIN differ?
2. Define state, action, branch, node, and terminal state in a game tree.
3. Trace one level of minimax backup on a two-ply example with MAX at the root.
4. Why is minimax optimal but impractical for chess and Go? Give approximate state-space sizes.
5. What does it mean for tic-tac-toe to be a "solved game"?
6. How does alpha-beta pruning avoid computing irrelevant branches? Define α and β.
7. How does move ordering affect alpha-beta pruning's effectiveness?
8. What is a heuristic evaluation function, and when is cutoff search used instead of full minimax?
9. Describe the four phases of Monte Carlo Tree Search.
10. How did AlphaGo combine neural networks with search, and what games have AI systems mastered?
