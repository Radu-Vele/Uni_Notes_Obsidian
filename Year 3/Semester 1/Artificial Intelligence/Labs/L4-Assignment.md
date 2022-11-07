# SMA*

> Idea = put a bound to the memory of the queue in A* and figure out how to memorize the deleted trees.

### Heuristic goal 
$$h(n) \le h^*(n)$$ where h*(n) is the actual distance to pacman.

The disadvantage of A* is that all the visited nodes are retained in memory

### MA*
$$f(n)=g(n)+h(n)$$
And the first pruned node is the one with the highest f

Two sets:
- CLOSED - nodes with successors in memory
- OPEN - nodes in memory

How to generate successors:
- take the node in OPEN with lowest f (PQ ish) and add its successors to OPEN

Event: number of nodes in OPEN + CLOSED reaches a limit
- remove from OPEN the node (leaf) with highest f. 

A new successor is generated:
- its f cost its propagated to the tree (to its ancestor $\Rightarrow$ ancestor contains info regfarding the f-costs of leaves)
```
e.g. 
if parent.f = 6 and if parent.descendant.f = 8 then
	parent.f = 8 
	//retained as lower bound regarding going down from parent
```


### SMA*
> [!Important] Improvements:
> - use a *BINARY TREE* to store The OPEN sorted by **f** and **Depth**
> - in a node, maintain 2 f-cost quantities ratger than 4
> - add and prune one node at a time

### Algorithm 🤔

```ruby
#Algorithm topLevel
Algorithm SMA * (start):
	put start on OPEN #binary tree DS probably - contains
	USED <- 1 #number of nodes in memory
	
	loop
		if OPEN.isEmpty() 
			return failure;
			
		best = OPEN.extract(deepest_leaf_with_least_f_cost)
	
		if best.isGoal() then
			return success; #We only have a goal state so it should be fine
	
		succ = best.nextSuccessor() #method has more information about
		#how to generate next successor
		
		succ.f = max(best.f, succ.g + succ.h) 
		#propagate the value of the parent if it s greater than f
	
		if best.completed() #there are no more unvisited children of best
			BACKUP(best);
	
		 
	
		USED = USED + 1 # used nodes in memory
	
		if(USED > MAX) then #case we need to prune nodes
			OPEN.pruneNode(the_shallowest, highest_f_cost_node)
			remove_from_parents_successors_list
			insert_its_parent_in_OPEN_if_necessary
			USED = USED - 1;
	
		OPEN.insert(succ)

# Propagates the cost of children to parents
Procedure BACKUP(n):
	if n is_completed and has a parent then
		f(n) = least_f_cost_of_all_successors
		if f(n) changed
			BACKUP(parent(n))
```

```ruby
# Calling the SMA* and initial steps
start_node = problem.getInitialState()
MAX = max_nr_of_nodes_to_be_accommodated
USED = how_many_nodes_are_now_in_memory

BT_NODE_STRUCTURE: (g, h, f, f_min_of_its_successors, info_on_next_successor_to_be_generated)

# successor that has not been generated since parent was last generated = unexamined
# node with all its sucessors examined is called complee

SMA*(start_node)
```

### OPEN set
- need to easily extract lowest depth highest f
- priority also set by f (update function)

---

### Wikipedia Algorithm
```ruby
function SMA-star(problem): path
  queue: set of nodes, ordered by f-cost;
begin
  queue.insert(problem.root-node);

  while True do begin
    if queue.empty() then 
	    return failure; #there is no solution that fits in the given memory
    node := queue.begin(); #min-f-cost-node
    
    if problem.is-goal(node) then 
	    return success;
    
    s := next-successor(node)
    
    if (!problem.is-goal(s) && depth(s) == max_depth) then
        f(s) := inf; 
        #there is no memory left to go past s, so the entire path is useless
    else
        f(s) := max(f(node), g(s) + h(s));
        # f-value of the successor is the maximum of
        #     f-value of the parent and 
        #     (heuristic of the successor + path length to the successor)
    end if
    
    if no more successors then
       update f-cost of node and those of its ancestors if needed
    
    if node.successors in queue then queue.remove(node);  # all children have already been added to the queue via a shorter way
    
    if memory is full then begin
		
		badNode := shallowest node with highest f-cost;
	    
	    for parent in badNode.parents do begin
	        parent.successors.remove(badNode);
        
	        if needed then 
		        queue.insert(parent); 
	      end for
    endif

    queue.insert(s);
    
  endwhile
end
```

# Other Search Algorithms:

## Options:
- Iterative Deepening DFS + Depth Limited Search - chosen
	- [x] Done
	- [ ] 
- Bidirectional Search
	- Using BFS
	- [x] Done
	- Using Astar

- Greedy BestFS

- IDA*

Local Search Algorithms:
- hill  climbing