# Temporal Event Pattern Mining and Rule Discovery

## Overview
This project focuses on temporal sequence mining of event log data to discover frequent patterns and generate temporal association rules. The workflow includes preprocessing, window-based sequence creation, sequential pattern mining, rule generation, and visualization of interestingness measures. The main goal is to analyze event logs and extract meaningful behavioral patterns over time.

## Key Features
- Load and preprocess event log data
- Convert timestamps into structured event sequences
- Perform window-based segmentation of event streams
- Mine frequent sequential patterns using PrefixSpan / sequential mining
- Generate temporal association rules
- Compute interestingness measures including support (frequency), confidence, recall, lift, and J-measure
- Analyze statistical relationships between rules
- Apply dimensionality reduction using PCA and UMAP
- Visualize rule distributions and clusters

## Dataset Description
The dataset is a tab-separated event log file containing the following columns:

- **RecordID**: Unique identifier for a user/session  
- **Category**: Type of event (e.g., resize, click, load, tooltip)  
- **Start Time**: Timestamp when the event occurred  
- **End Time**: Timestamp when the event ended (optional)  
- **Attributes**: Additional metadata describing the event  

## Installation
The following Python packages are required:

```bash
pip install prefixspan
pip install pymining
pip install umap-learn
pip install pandas numpy scikit-learn matplotlib seaborn
Pipeline Steps
Data Loading
```
The dataset is loaded using pandas from a tab-separated file. A subset of rows may be used for testing.

#Timestamp Conversion

Start Time is converted into datetime format to enable temporal analysis.

#Windowing of Events

Events are grouped into fixed time windows based on a maximum span (e.g., 10 seconds) and step size (e.g., 5 seconds).
Each window contains a sequence of event categories.

-Example sequence:

appInit → resize → toolTip → create
Sequential Pattern Mining

Frequent sequential patterns are extracted using PrefixSpan / PyMining.
Patterns represent recurring sequences of events along with their frequency.

-Examples:

resize → resize (939 occurrences)
readBoundData (1674 occurrences)
appInit → resize (479 occurrences)
Temporal Rule Generation

Frequent patterns are converted into temporal association rules:

X → Y

Where:

X = antecedent sequence
Y = consequent event

#Metrics used:

-Support (frequency)
-Confidence
-Recall
-Lift
-J-measure
-Rule Filtering

Rules are filtered using thresholds such as high lift and high confidence to identify strong relationships.

#Visualization
-Correlation matrix of interestingness measures
-Pairplot of rule metrics
-PCA projection (2D)
-UMAP embedding for clustering

#Outputs
-Frequent sequential patterns
-Temporal association rules
-Ranked rule list
-Statistical summaries
-PCA and UMAP visualizations

#Insights
-Strong self-repetition patterns (e.g., resize → resize)
-System events like readBoundData and toolTip are highly frequent
-UI interaction loops appear in high-confidence rules
-Clusters of similar behavioral patterns are visible in embeddings

#Limitations
-Self-repeating events may inflate metrics (confidence/lift)
-Support is approximated from mined patterns
-Fixed windows may not reflect real user sessions
-UMAP may produce sparse or disconnected clusters

#Future Improvements
-Use session-based segmentation instead of fixed windows
-Normalize repeated consecutive events
-Compute support from raw sequences
-Improve pattern mining using direct PrefixSpan outputs
-Add anomaly detection for rare sequences
-Use sequence embeddings for better clustering

#Technologies Used
-Python
-Pandas
-PrefixSpan / PyMining
-Scikit-learn
-UMAP
-Matplotlib
-Seaborn
