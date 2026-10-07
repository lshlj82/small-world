# The Small-World Effect: An Interactive Demo

An in-browser demo of the mathematics behind the small-world effect. It covers trees and breadth-first search, distance and the average path length, why lattices are large worlds (⟨ℓ⟩ ∝ N^½) while random networks are small worlds (⟨ℓ⟩ ∼ log N), the Watts–Strogatz model, and the clustering coefficient versus transitivity.

Created by Claude Opus 5.5, based on the lecture slides by Sang Hoon Lee.

## What's inside

The page is a single self-contained `index.html`. It has no build step. Its only outside resources are two Google Fonts (Source Serif 4 and IBM Plex Sans) and KaTeX 0.16.9 from cdnjs, which typesets the formulas. Without them the page falls back to system fonts and shows the formulas as plain TeX. All networks are generated and measured in the browser; the karate club and college football networks are embedded in the file. It shares its look and chart code with the companion scale-free, centrality and friendship-paradox demos.

The demo has seven parts:

1. **How many steps away?** Five networks of about 400 people with about four friends each: a 20 × 20 lattice, a ring lattice, the same ring with 5% of its links rewired, random links, and the karate club. Click anyone to color everyone by their distance and see the histogram of distances. The 2D lattice shows the Manhattan diamonds. The summary compares ⟨ℓ⟩ across the networks: 50 for the ring, 13 for the lattice, 9.5 for the rewired ring and 4.4 for random links.
2. **Trees.** A 15-node tree drawn in layers. Click any node to make it the root, click a link to cut it, or add random links. A panel tracks N, L, the number of pieces, the number of independent cycles L − N + (pieces), and whether the network is a tree.
3. **Breadth-first search.** A step-by-step run on a 13-node network. It shows the frontier queue, the distance assigned to each node, the step of the algorithm being executed, and the directed shortest-path tree growing in orange. You can step, play or restart from any source.
4. **Distance and ⟨ℓ⟩.** The directed seven-node example from the slides with ℓ(1→2) = 1, ℓ(1→7) = 2 and ℓ(1→6) = 4. The full distance matrix shows the asymmetry and the unreachable pairs that make ⟨ℓ⟩ infinite. Clicking a cell draws the path.
5. **Large and small worlds.** ⟨ℓ⟩ measured from N = 100 to 100,000 for a ring lattice, a 2D lattice, a rewired ring and random links, against the predictions N/8, (2/3)√N and ln N/ln⟨k⟩, on linear or logarithmic axes. A second chart compares ln N with N^α for an adjustable α and finds where the power finally wins, around N ≈ 10^16 for α = 0.1.
6. **Where the logarithm comes from.** The number of nodes in each layer around a source, measured by breadth-first search on 10,000-node networks. Each is compared with the tree estimate: k(k − 1)^(n−1) exactly for a Cayley tree, ⟨k⟩^n for random links, and 4n for the lattice, where loops cannot be ignored.
7. **Watts–Strogatz and clustering.** A 20-node ring rewires as you move p, next to C(p)/C(0) and L(p)/L(0) for 1,000 nodes with 10 neighbors each, as in the 1998 paper. An ego network lets you link or unlink pairs of friends and watch C(i) = 2τ(i)/(k_i(k_i − 1)). For whole networks, the page compares C averaged over nodes with k > 1, NetworkX's `average_clustering`, the transitivity T = 3 × triangles / triads, and the random-network value ⟨k⟩/(N − 1). The four-node example gives C = 5/6 and T = 3/4. The karate club gives 45 triangles, 528 triads, T = 0.2557 and an average clustering of 0.5706, as on the slides.

## Running it

Open `index.html` in any modern browser. To host it with GitHub Pages, push this folder as a repository and enable Pages for the branch that contains `index.html`.

## Models and methods

- **Distances** come from breadth-first search. The 400-node networks at the top use every source. The scaling and Watts–Strogatz curves average over 30 and 80 random sources respectively, in the largest connected component.
- **Random networks** use the G(N, M) model with M = N⟨k⟩/2 links placed uniformly at random.
- **Lattices** are square grids with open boundaries. Ring lattices link each node to its k/2 nearest neighbors on each side.
- **Watts–Strogatz rewiring** moves one end of each ring link, with probability p, to a uniformly random node, avoiding self-loops and duplicate links. Each link's random draws are fixed, so raising p only adds rewirings and the drawing changes smoothly.
- **The Cayley tree** has k = 3 and 12 layers (12,286 nodes).
- **Clustering** counts triangles exactly. C(i) is undefined for k_i < 2. C averages over nodes with k > 1, while NetworkX's `average_clustering` counts those nodes as zero. Triads are Σ_i k_i(k_i − 1)/2 = (Σk_i² − Σk_i)/2.

## References

- F. Menczer, S. Fortunato, and C. A. Davis, *A First Course in Network Science* (Cambridge University Press, 2020), Chapter 2.
- D. J. Watts and S. H. Strogatz, "Collective dynamics of 'small-world' networks," *Nature* 393, 440 (1998).
- S. Milgram, "The small world problem," *Psychology Today* 1, 61 (1967).
- W. W. Zachary, *J. Anthropol. Res.* 33, 452 (1977); M. Girvan and M. E. J. Newman, *Proc. Natl. Acad. Sci. USA* 99, 7821 (2002).
