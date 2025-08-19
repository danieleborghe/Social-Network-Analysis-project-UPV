# Social Network Analysis of the Spotify Artist Collaboration Network

This repository contains a comprehensive Social Network Analysis (SNA) project focused on the collaboration network between artists on Spotify. We analyze the structure of this vast network to identify key influencers, uncover community structures based on musical genres, and assess the network's resilience to disruptions.

This project was developed for the "Social Network Analysis" course at the **Universitat Politècnica de València (UPV)**.

[![Read the Presentation](https://img.shields.io/badge/Read_the_Full-Presentation-red?style=for-the-badge&logo=microsoftpowerpoint)](presentation%20SNA.pdf)

---

## 📝 Table of Contents

- [Project Goal: Mapping the Music Industry's Connections](#-project-goal-mapping-the-music-industrys-connections)
- [Methodology: A Graph-Based Approach to Music](#-methodology-a-graph-based-approach-to-music)
- [Technical Stack & Tools](#-technical-stack--tools)
- [The Dataset: A Sprawling Network of Artists](#-the-dataset-a-sprawling-network-of-artists)
- [Analysis Workflow & Techniques](#-analysis-workflow--techniques)
- [Key Findings & Insights](#-key-findings--insights)
- [Repository Structure](#-repository-structure)
- [How to Run This Project](#-how-to-run-this-project)
- [Author](#-author)

---

## 🎯 Project Goal: Mapping the Music Industry's Connections

The music industry is a highly interconnected ecosystem where collaborations define genres, drive trends, and launch careers. This project aims to model and analyze these connections by treating the Spotify artist "feature" landscape as a massive social network.

Our primary research questions are:
-   Who are the most central and influential artists connecting different parts of the music world?
-   Do artists form distinct communities, and do these clusters correspond to specific genres or regions?
-   How robust is the collaboration network? What happens if key artists are removed, either randomly or through targeted "attacks"?

---

## 💡 Methodology: A Graph-Based Approach to Music

We model the artist collaboration network as a **graph**, where each **node** is an artist and an **edge** represents a feature collaboration between two artists. This powerful abstraction allows us to apply a suite of SNA techniques to uncover patterns that are invisible at a surface level.

Due to the immense size of the original network, a key part of our methodology was **network sampling**. We created smaller, representative subgraphs to make complex computations (like community detection and fault tolerance analysis) feasible on standard hardware.

---

## 💻 Technical Stack & Tools

This project utilizes a standard Python-based stack for network analysis and data science.

-   **Language**: **Python 3.x**
-   **Core Libraries**:
    -   **`pandas`** & **`numpy`**: For data loading, cleaning, and manipulation.
    -   **`networkx`**: The primary library for creating, manipulating, and analyzing graph structures.
    -   **`matplotlib`** & **`seaborn`**: For plotting distributions and visualizing results.
-   **Analysis Algorithms**:
    -   **Centrality Measures**: Degree, Closeness, Betweenness, Eigenvector, PageRank, and HITS (Hubs & Authorities).
    -   **Community Detection**: **Girvan-Newman** algorithm for identifying densely connected subgroups.
-   **Visualization Software**:
    -   **`Cytoscape`**: An open-source platform used for advanced, interactive network visualization.

---

## 📊 The Dataset: A Sprawling Network of Artists

The full dataset captures a significant portion of the Spotify ecosystem:
-   **Nodes**: Approximately **150,000 artists**.
-   **Edges**: Over **300,000 collaborations**.

To manage this scale, we worked with two primary samples:
-   **Sample 1**: ~10,000 nodes and ~12,000 edges, used for preliminary and centrality analyses.
-   **Sample 2**: ~900 nodes and ~700 edges, used for the more computationally intensive community detection and fault tolerance simulations.

---

## ⚙️ Analysis Workflow & Techniques

Our analysis followed a structured, multi-stage workflow to progressively deepen our understanding of the network.

1.  **Data Preparation and Sampling**: The initial phase involved cleaning the data and developing a sampling strategy to create manageable subgraphs.

2.  **Centrality Analysis**: We calculated a wide range of centrality metrics to identify the most important artists in the network. This helped us pinpoint key figures who are highly popular, act as bridges between communities, or are connected to other influential artists.

3.  **Community Detection**:
    -   **Goal**: To discover how the music world naturally clusters into communities.
    -   **Method**: We applied the **Girvan-Newman algorithm** on our smaller sample to partition the network.
    -   **Analysis**: We analyzed the resulting communities to understand their composition, identifying clusters corresponding to a "diverse urban and pop scene," "electronic and alternative fusion," a "vibrant Latin music hub," and others.

4.  **Robustness and Fault Tolerance**:
    -   **Goal**: To assess the network's resilience by simulating the removal of artists.
    -   **Scenarios**:
        -   **Random Failure**: Simulating an unexpected event where a random group of artists is removed.
        -   **Targeted Attack**: Simulating a coordinated event where the most influential (most central) artists are removed.
    -   **Metrics**: We measured the impact by observing changes in the **Giant Component size**, **Clustering Coefficient**, and **Average Shortest Path Length**.

---

## 📈 Key Findings & Insights

-   **Identification of Key Influencers**: Centrality analysis revealed a diverse set of influential artists, including **Diplo**, **Snoop Dogg**, and **Anitta**, each playing a different structural role in the network (e.g., high degree vs. high betweenness).
-   **Genre-Based Communities**: The Girvan-Newman algorithm successfully identified meaningful communities that strongly align with musical genres and geographical regions, such as Indian fusion, Latin music, and German pop.
-   **Network Fragility**: The fault tolerance analysis demonstrated that the network is relatively resilient to random failures but **highly vulnerable to targeted attacks**. The removal of just a few central artists caused a **dramatic collapse of the giant component** and severe fragmentation of the network.
-   **The Importance of Hubs**: This project empirically confirms the critical role of highly connected "hub" artists in maintaining the cohesion and connectivity of the global music scene. Their removal has a disproportionately large impact on collaboration opportunities across the entire network.

---

## 📂 Repository Structure

```

.
├── data/
│   ├── nodes.csv          \# Full dataset of artists (nodes)
│   └── edges.csv          \# Full dataset of collaborations (edges)
├── analysis\_part\_1.ipynb  \# Notebook for global analysis and centrality measures
├── analysis\_part\_2.ipynb  \# Notebook for community detection and fault tolerance
├── centrality\_measures.csv  \# CSV output of node centrality scores
├── cytoscape.cys          \# Cytoscape session file for visualization
├── presentation SNA.pdf   \# The final project presentation
└── README.md              \# This file

````

---

## 🚀 How to Run This Project

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/danieleborghe/Social-Network-Analysis-project-UPV.git](https://github.com/danieleborghe/Social-Network-Analysis-project-UPV.git)
    cd Social-Network-Analysis-project-UPV
    ```

2.  **Set up a virtual environment and install dependencies:**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
    pip install pandas numpy networkx matplotlib seaborn jupyter
    ```

3.  **Launch Jupyter Notebook:**
    ```bash
    jupyter notebook
    ```

4.  **Run the Notebooks:**
    -   Open and run `analysis_part_1.ipynb` and `analysis_part_2.ipynb` to replicate the analyses. *Note: Running on the full dataset may be slow; the notebooks are likely configured to use smaller samples.*

5.  **Explore in Cytoscape (Optional):**
    -   Install [Cytoscape](https://cytoscape.org/).
    -   Import the edge and node CSV files to create and explore interactive visualizations of the network.

---

## ✍️ Author

- **Daniele Borghesi**
