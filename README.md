# Community-Aware Product Recommendation using Louvain Algorithm on Amazon Co-Purchasing Network

This repository contains the implementation of community detection and recommendation systems for product co-purchasing networks, leveraging the Louvain algorithm to enhance recommendation relevance and quality.

## Overview

This project applies network science methodologies to analyze product co-purchasing patterns on Amazon's product network using the CRISP-DM framework. We constructed a graph representation with 259,102 products (nodes) and 879,700 co-purchasing relationships (edges), then applied the Louvain community detection algorithm to identify meaningful product communities. Our analysis revealed 190 distinct communities representing coherent product categories, which we leveraged to enhance recommendation systems.

## Features

- **Data Preparation**: Comprehensive data cleaning and preprocessing for co-purchase networks
- **Graph Analysis**: Construction and analysis of product co-purchasing networks
- **Community Detection**: Implementation of the Louvain algorithm for identifying product communities
- **Recommendation Systems**: Three recommendation approaches:
  - Basic neighbor-based recommendations
  - Community-aware recommendations
  - Advanced model incorporating popularity and rating metrics
- **Evaluation**: Metrics for measuring recommendation quality (precision, recall, F1-score)
- **Visualization**: Network visualization with community coloring

## Requirements

The implementation requires the following Python libraries:
- pandas
- numpy
- networkx
- matplotlib
- seaborn
- multiprocessing (standard library)

## Installation and Usage

1. Clone this repository
   ```
   git clone https://github.com/username/Community-Aware-Product-Recommendation.git
   cd Community-Aware-Product-Recommendation
   ```

2. Install required dependencies:
   ```
   pip install pandas numpy networkx matplotlib seaborn
   ```

3. Prepare your data files:
   - `copurchase.csv`: Contains co-purchasing relationships (Source, Target, optional Weight)
   - `products.csv`: Contains product information (id, title, group, etc.)

4. Run the analysis:
   ```
   python louvain.py
   ```

5. Examine the output files:
   - `analysis_output_[timestamp].txt`: Detailed analysis results
   - `product_recommendations_[timestamp].txt`: Generated product recommendations
   - `copurchase_graph.png`: Visualization of the network with community colors

## Methodology

### Data Preparation
The implementation handles data cleaning, type conversion, and feature engineering to prepare the co-purchasing data for analysis. Key steps include:
- Removing missing values, duplicates, and self-loops
- Ensuring data type consistency between datasets
- Creating features for network connectivity: outgoing count, incoming count, and total connections
- Sampling strategies for computational efficiency with large graphs

### Community Detection
We implemented the Louvain method for community detection, which optimizes modularity - a metric that measures the density of connections within communities relative to connections between communities. The algorithm operates through a two-phase iterative process:
1. Local optimization: Nodes are moved between communities to maximize modularity gain
2. Network aggregation: Nodes in the same community are aggregated into "super-nodes"

The implementation includes fallback options for large or disconnected graphs, using label propagation or fluid communities algorithms when necessary.

### Recommendation Approaches
1. **Basic Neighbor-based**: Recommends products directly connected in the co-purchasing network, weighted by connection strength
2. **Community-aware**: Enhances recommendations by boosting scores for products within the same community
3. **Advanced Model**: Incorporates multiple factors including:
   - Direct and second-degree connections
   - Community membership
   - Product popularity
   - User ratings

## Evaluation Results

Our three recommendation approaches were evaluated using precision, recall, and F1-score metrics:

| Metric | Basic | Community-aware | Advanced |
|--------|-------|-----------------|----------|
| Precision | 0.9960 | 0.9960 | 0.8920 |
| Recall | 0.8093 | 0.8093 | 0.7332 |
| F1 Score | 0.8930 | 0.8930 | 0.8048 |

While the basic and community-aware approaches achieved identical high precision (0.9960), qualitative analysis showed that community-aware recommendations were more thematically consistent. The advanced model showed slightly lower precision (0.8920) but produced more diverse recommendations that sometimes crossed community boundaries.

Through empirical evaluation using influential products, we observed that recommendations within the same community exhibited stronger contextual relevance despite similar quantitative metrics.

## Key Insights

- **Community coherence produces better recommendations**: Community structure captures semantic relationships beyond mere co-purchasing frequencies
- **Different communities exhibit distinct co-purchasing patterns**: Book-dominated communities show tighter thematic connections, while electronics communities show more accessory-based connections
- **High precision translates to business impact**: The high precision (0.996) achieved means nearly every recommended product has been empirically observed to be purchased with the seed product

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