# Social Network Analysis of Portuguese Twitch Streamers

This repository contains a comprehensive Social Network Analysis (SNA) of the community of Portuguese-speaking streamers on Twitch. The project constructs a network graph based on mutual following relationships to analyze its structure, identify key influencers, and uncover community clusters.

This project was developed for the "Social Network Analysis" course at the **Universitat Politècnica de València (UPV)**.

[![Read the Presentation](https://img.shields.io/badge/Read_the_Full-Presentation-red?style=for-the-badge&logo=microsoftpowerpoint)](presentation%20SNA.pdf)

---

## 📝 Table of Contents

- [Project Goal: Mapping the Twitch PT Community](#-project-goal-mapping-the-twitch-pt-community)
- [The Dataset: A Snapshot of Twitch Portugal](#-the-dataset-a-snapshot-of-twitch-portugal)
- [Technical Stack & Tools](#-technical-stack--tools)
- [Analysis Workflow & Methodologies](#-analysis-workflow--methodologies)
- [Key Findings & Insights](#-key-findings--insights)
- [Repository Structure](#-repository-structure)
- [How to Run the Analysis](#-how-to-run-the-analysis)
- [Authors](#-authors)

---

## 🎯 Project Goal: Mapping the Twitch PT Community

Twitch is a massive platform where communities form around content creators. This project aims to move beyond simple viewership metrics to understand the underlying social structure of the Portuguese-speaking Twitch scene.

Our main objectives are:
-   **Construct and Visualize** the social network graph of Twitch PT streamers.
-   **Analyze the Network's Topology**: Understand its overall properties, such as density, connectivity, and centralization.
-   **Identify Key Influencers**: Use centrality measures to find the most important and influential streamers in the network.
-   **Discover Community Structures**: Apply community detection algorithms to identify sub-groups or "cliques" of streamers who are more interconnected with each other than with the rest of the network.
-   **Compare to Theoretical Models**: Determine if the network follows patterns of known graph models (like scale-free or small-world networks).

---

## 📊 The Dataset: A Snapshot of Twitch Portugal

The dataset for this project was sourced from the Twitch API and captures the network of Portuguese-speaking streamers.

-   **Nodes**: Represent individual Twitch streamers (13,853 unique streamers).
-   **Edges**: Represent a **mutual follow** relationship between two streamers. An edge exists if Streamer A follows Streamer B AND Streamer B follows Streamer A (24,797 mutual connections).
-   **Attributes**: Node attributes include `language`, `creation date`, `total views`, and `mature content` flag.

The graph is treated as **undirected**, since the follow relationship is mutual.

---

## 💻 Technical Stack & Tools

-   **Language**: **Python 3.x**
-   **Core Libraries**:
    -   **Pandas**: For data loading, cleaning, and manipulation of the node and edge lists.
    -   **NetworkX**: The primary library for creating the graph object, performing all network analyses, and calculating metrics.
    -   **Matplotlib** & **Seaborn**: For plotting distributions and statistical charts.
-   **Network Visualization**:
    -   **Cytoscape**: Used for high-quality, interactive visualization of the network graph. It allows for advanced styling, layout algorithms, and exploration that are not possible with standard Python plotting libraries.

---

## ⚙️ Analysis Workflow & Methodologies

The project is divided into a systematic, multi-step analysis workflow.

1.  **Network Construction and Preprocessing**
    -   Loading the raw node and edge CSV files.
    -   Cleaning the data by removing isolated nodes (streamers with no mutual connections) to focus on the main network structure.
    -   Constructing the graph object using NetworkX.

2.  **Global Network Analysis**
    -   **Basic Metrics**: Calculating the number of nodes and edges, network density, and average degree.
    -   **Connectivity**: Identifying connected components to see if the network is fragmented or cohesive. The analysis focuses on the **Giant Connected Component (GCC)**.
    -   **Pathways**: Computing the network's diameter and average shortest path length to understand information flow efficiency.

3.  **Centrality Analysis (Identifying Key Players)**
    -   **Degree Centrality**: To find streamers with the most direct connections (the most popular or "gregarious").
    -   **Betweenness Centrality**: To find "bridges" or "brokers" who connect different parts of the network.
    -   **Closeness Centrality**: To find streamers who can spread information most efficiently across the network.
    -   **Eigenvector Centrality**: To find streamers who are connected to other highly connected streamers (influencers within influential circles).

4.  **Community Detection**
    -   **Goal**: To partition the network into communities or modules.
    -   **Algorithm**: We use the **Louvain Modularity** algorithm, a highly efficient method for detecting community structures in large networks.

5.  **Network Modeling**
    -   **Goal**: To understand the underlying principles of the network's formation.
    -   **Comparison**: We compare the degree distribution of our real-world Twitch network against two theoretical models:
        -   **Erdős-Rényi (ER) Model**: A random graph model.
        -   **Barabási-Albert (BA) Model**: A model that generates scale-free networks through preferential attachment.

---

## 📈 Key Findings & Insights

-   **Small-World, Scale-Free Network**: The Twitch PT network exhibits classic "small-world" properties (high clustering, short average path lengths) and follows a **power-law degree distribution**, characteristic of a **scale-free network**. This means a few streamers ("hubs") have a massive number of connections, while most have very few.
-   **Identified Hubs**: Centrality analysis successfully identified the top streamers who act as the main hubs and information brokers of the community. These are often the largest and most well-known content creators.
-   **Strong Community Structure**: The Louvain algorithm detected **16 distinct communities**, indicating that the network is not uniform but rather a collection of tighter sub-groups, likely formed around specific games, content types, or streamer friendships.
-   **Preferential Attachment**: The network's structure is much better explained by the Barabási-Albert model than the random ER model. This confirms that the network grows via **preferential attachment**: new or smaller streamers are more likely to connect with already popular streamers, reinforcing their central position.

---

## 📂 Repository Structure

```

.
├── data/
│   ├── nodes.csv              \# Raw list of streamers
│   ├── edges.csv              \# Raw list of connections
│   ├── cleaned\_nodes.csv        \# Nodes after preprocessing
│   └── cleaned\_edges.csv        \# Edges after preprocessing
├── figures/
│   └── ...                    \# PNG images of network visualizations
├── part\_1.ipynb                 \# Jupyter Notebook for data prep and centrality analysis
├── part\_2.ipynb                 \# Jupyter Notebook for community detection and network models
├── presentation SNA.pdf         \# The final project presentation
├── cytoscape.cys                \# Cytoscape session file for interactive visualization
├── network\_measures.csv         \# CSV with global network metrics
├── centrality\_measures.csv      \# CSV with node-level centrality scores
└── README.md                    \# This file

````

---

## 🚀 How to Run the Analysis

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/danieleborghe/Social-Network-Analysis-project-UPV.git](https://github.com/danieleborghe/Social-Network-Analysis-project-UPV.git)
    cd Social-Network-Analysis-project-UPV
    ```

2.  **Set up a virtual environment and install dependencies:**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
    pip install pandas networkx matplotlib seaborn jupyter
    ```

3.  **Launch Jupyter Notebook:**
    ```bash
    jupyter notebook
    ```

4.  **Run the Notebooks:**
    -   Open and run `part_1.ipynb` to perform the initial data cleaning, network construction, and centrality analysis.
    -   Open and run `part_2.ipynb` to perform community detection and compare the network to theoretical models.

5.  **Explore in Cytoscape (Optional):**
    -   Download and install [Cytoscape](https://cytoscape.org/).
    -   Open the `cytoscape.cys` file to explore the fully visualized and styled network graph.

---

## 👥 Authors

- **Daniele Borghesi**
- **Eva Cantin Larumbe**
- **Eva Teisberg**
- **Mikel Baraza Vidal**
- **Francesco Pio Capoccello**
