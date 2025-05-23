# Community-Aware Product Recommendation using Louvain Algorithm on Amazon Co-Purchasing Network

This repository contains the implementation of community detection and recommendation systems for product co-purchasing networks, as detailed in our paper "Community Detection and Recommendation Systems in Product Co-Purchasing Networks".

## Overview

This project applies network science methodologies to analyze product co-purchasing patterns using the CRISP-DM framework. We constructed a graph representation of Amazon's product co-purchasing network with 259,102 products (nodes) and 879,700 co-purchasing relationships (edges), then applied the Louvain community detection algorithm to identify meaningful product communities.

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

## Installation and Usage

1. Clone this repository
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

## Implementation Details

### Data Preparation
The implementation handles data cleaning, type conversion, and feature engineering to prepare the co-purchasing data for analysis. Key steps include handling missing values, removing duplicates, and calculating connectivity metrics.

### Community Detection
We implemented the Louvain method for community detection with fallback options for large or disconnected graphs. The algorithm optimizes modularity, a metric that measures the density of connections within communities relative to connections between communities.

### Recommendation Approaches
1. **Basic Neighbor-based**: Recommends products directly connected in the co-purchasing network
2. **Community-aware**: Enhances recommendations by boosting scores for products within the same community
3. **Advanced Model**: Incorporates multiple factors including community membership, product popularity, and ratings

### Sampling Strategy
For computational efficiency with large graphs, we implemented strategic sampling approaches described in Section 3.3 of the paper, using fixed random seeds to ensure reproducibility.

## Results

Our analysis revealed 190 distinct communities representing coherent product categories. The three recommendation approaches were evaluated, with both basic and community-aware approaches achieving identical high precision (0.9960), while the advanced model showed slightly lower precision (0.8920) but potentially greater recommendation diversity.

Through empirical evaluation using influential products, we observed that recommendations within the same community exhibited stronger contextual relevance despite similar quantitative metrics.


## Contributors
- Kevin Ignatius Wijaya


## License

This project is available for academic and research purposes.