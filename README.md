# Community-Aware Product Recommendation using Louvain Algorithm on Amazon Co-Purchasing Network

This repository implements community detection and recommendation systems for e-commerce product networks, leveraging the Louvain algorithm to enhance recommendation relevance through network structure analysis.

## Research Motivation

E-commerce platforms rely on understanding how products are purchased together to provide relevant recommendations. This research analyzes Amazon's co-purchasing network to:

1. Identify natural communities of products frequently purchased together
2. Evaluate how community structure can enhance recommendation systems
3. Demonstrate improved contextual relevance through community-aware recommendations
4. Provide a framework for analyzing large-scale product networks

## Overview

This project applies network science methodologies to analyze product co-purchasing patterns on Amazon's product network using the CRISP-DM framework. We constructed a graph representation with 259,102 products (nodes) and 879,700 co-purchasing relationships (edges), then applied the Louvain community detection algorithm to identify meaningful product communities. Our analysis revealed 190 distinct communities representing coherent product categories, which we leveraged to enhance recommendation systems.

## Methodology

### Data Preparation

The implementation handles comprehensive data preparation tasks including:

- Cleaning and preprocessing co-purchasing data
- Removing missing values, duplicates, and self-loops
- Ensuring data type consistency between datasets
- Creating network connectivity features (outgoing count, incoming count, total connections)
- Implementing sampling strategies for computational efficiency

For large-scale networks, we employ neighbor sampling as our primary approach, which preserves co-purchase relationships while making computation feasible. This method directly captures product relationships by sampling nodes and their immediate neighbors, better representing local structures that are crucial for understanding product associations.

### Graph Construction

We construct a directed graph where:
- Nodes represent individual products
- Edges represent co-purchasing relationships
- Edge weights represent the strength of co-purchasing relationship

The graph implementation handles both weighted and unweighted scenarios, with fallback options for large or disconnected graphs.

### Community Detection

We implemented the Louvain method for community detection, which optimizes modularity - a metric that measures the density of connections within communities relative to connections between communities. The algorithm operates through a two-phase iterative process:

1. **Local optimization**: Nodes are moved between communities to maximize modularity gain, defined as:

   Q = (1/2m) ∑ᵢⱼ [Aᵢⱼ - (kᵢkⱼ/2m)] δ(cᵢ,cⱼ)

   where Aᵢⱼ represents edge weight, kᵢ is the sum of weights of edges attached to node i, cᵢ is the community of node i, and m is the sum of all edge weights.

2. **Network aggregation**: Nodes in the same community are aggregated into "super-nodes" and a new network is constructed.

This approach identified 190 distinct communities in our network, revealing a highly structured product ecosystem with both category coherence and interesting cross-category relationships.

### Recommendation Approaches

We developed and evaluated three recommendation approaches:

1. **Basic Neighbor-based**: Recommends products directly connected in the co-purchasing network, weighted by connection strength.

2. **Community-aware**: Enhances the basic approach by boosting scores for products within the same community as the input product:
   ```python
   if partition and product_id in partition:
       product_community = partition[product_id]
       for node, score in list(scores.items()):
           if node in partition and partition[node] == product_community:
               scores[node] = score * (1 + community_weight)
   ```

3. **Advanced Model**: Incorporates multiple factors including:
   - Direct and second-degree connections
   - Community membership with weighted boosting
   - Product popularity normalization
   - User ratings as a quality signal

## Key Findings

### Community Structure Analysis

The Louvain algorithm identified 190 distinct communities with varying sizes. The largest five communities contained 15,605, 11,021, 10,970, 9,785, and 8,273 products respectively. Analysis revealed:

1. **Category coherence**: Most communities contained products from related categories (e.g., thematically related books or music)
2. **Cross-category relationships**: Many communities revealed purchasing patterns crossing traditional category boundaries
3. **Community hub products**: Each community typically contained highly connected "hub" products linking subcommunities

### Recommendation Evaluation

Our evaluation using precision, recall, and F1-score metrics showed:

| Metric | Basic | Community-aware | Advanced |
|--------|-------|-----------------|----------|
| Precision | 0.9200 | 0.9200 | 0.7160 |
| Recall | 0.6738 | 0.6738 | 0.6327 |
| F1 Score | 0.7779 | 0.7779 | 0.6718 |
| Coverage | 0.0007 | 0.0007 | 0.0008 |

While the basic and community-aware approaches achieved identical precision (0.92), qualitative analysis showed that community-aware recommendations were more thematically consistent. The advanced model showed slightly lower precision (0.716) but produced more diverse recommendations that sometimes crossed community boundaries.

### Key Insights from Recommendations

- **Community coherence improves recommendation quality**: Community structure captures semantic relationships beyond mere co-purchasing frequencies
- **Different communities exhibit distinct patterns**: Book-dominated communities show tighter thematic connections, while electronics communities show more accessory-based connections
- **High precision translates to business impact**: The high precision achieved means nearly every recommended product has been empirically observed to be purchased with the seed product

## Installation and Usage

### Requirements

The implementation requires the following Python libraries:
- pandas
- numpy
- networkx
- matplotlib
- seaborn
- multiprocessing (standard library)

### Installation

1. Clone this repository
   ```
   git clone https://github.com/username/Community-Aware-Product-Recommendation.git
   cd Community-Aware-Product-Recommendation
   ```

2. Install required dependencies:
   ```
   pip install pandas numpy networkx matplotlib seaborn
   ```

### Usage

1. Prepare your data files:
   - `copurchase.csv`: Contains co-purchasing relationships (Source, Target, optional Weight)
   - `products.csv`: Contains product information (id, title, group, etc.)

2. Run the analysis:
   ```
   python louvain.py
   ```

3. Examine the output files:
   - `analysis_output_[timestamp].txt`: Detailed analysis results
   - `product_recommendations_[timestamp].txt`: Generated product recommendations
   - `copurchase_graph.png`: Visualization of the network with community colors

## Code Structure

The implementation follows a modular structure:

- **Data Preparation**: `load_and_prepare_data()` handles data cleaning, type conversion, and feature engineering
- **Graph Construction**: `create_graph()` builds the network representation
- **Community Detection**: `detect_communities()` implements the Louvain method with fallbacks
- **Recommendation Systems**: 
  - `recommend_products_enhanced()` - Basic and community-aware recommendation
  - `recommend_products_advanced()` - Advanced multi-factor recommendation
- **Evaluation**: `evaluate_recommendations()` measures precision, recall, and F1-score

## Future Work

- Exploring temporal dynamics to understand how product communities evolve over time
- Integrating customer segmentation data to create personalized community-aware recommendations
- Conducting A/B testing to measure the real-world impact on sales metrics
- Developing hybrid approaches that balance precision and diversity more effectively

## References

- Blondel, V. D., Guillaume, J. L., Lambiotte, R., & Lefebvre, E. (2008). Fast unfolding of communities in large networks.
- Linden, G., Smith, B., & York, J. (2003). Amazon.com recommendations: Item-to-item collaborative filtering.
- Shearer, C. (2000). The CRISP-DM model: The new blueprint for data mining.
- Sarwar, B., Karypis, G., Konstan, J., & Riedl, J. (2001). Item-based collaborative filtering recommendation algorithms.
- Huang, Z., Zeng, D. X., & Chen, H. (2007). Analyzing consumer-product graphs: Empirical findings and applications in recommender systems.
- Shokrzadeh, Z., Feizi-Derakhshi, M. R., Balafar, M. A., & Bagherzadeh-Mohasefi, J. (2022). Graph-based recommendation system enhanced with community detection.

## Contributors
- Kevin Ignatius Wijaya
- Iqza Ardiansyah
- Hanan Adipratama
- Muhammad Nabiel Subhan
- Muhammad Fauzan Jaisyurrahman
- Kevin Alexander
- Timothy Orvin Edwardo
- Andi Pujo Rahadi