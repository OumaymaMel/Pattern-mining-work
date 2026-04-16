TEMPORAL EVENT PATTERN MINING AND RULE DISCOVERY

OVERVIEW
This project focuses on temporal sequence mining of event log data to discover frequent patterns and generate temporal association rules. The workflow includes preprocessing, window-based sequence creation, sequential pattern mining, rule generation, and visualization of interestingness measures. The main goal is to analyze event logs and extract meaningful behavioral patterns over time.

KEY FEATURES

Load and preprocess event log data
Convert timestamps into structured event sequences
Perform window-based segmentation of event streams
Mine frequent sequential patterns using PrefixSpan / sequential mining
Generate temporal association rules
Compute interestingness measures including support (frequency), confidence, recall, lift, and J-measure
Analyze statistical relationships between rules
Apply dimensionality reduction using PCA and UMAP
Visualize rule distributions and clusters

DATASET DESCRIPTION
The dataset is a tab-separated event log file containing the following columns:

RecordID: Unique identifier for a user/session
Category: Type of event (e.g., resize, click, load, tooltip)
Start Time: Timestamp when the event occurred
End Time: Timestamp when the event ended (optional)
Attributes: Additional metadata describing the event

INSTALLATION
The following Python packages are required:

pip install prefixspan
pip install pymining
pip install umap-learn
pip install pandas numpy scikit-learn matplotlib seaborn

PIPELINE STEPS

DATA LOADING
The dataset is loaded using pandas from a tab-separated file. A subset of rows may be used for testing.
TIMESTAMP CONVERSION
Start Time is converted into datetime format to enable temporal analysis.
WINDOWING OF EVENTS
Events are grouped into fixed time windows based on a maximum span (e.g., 10 seconds) and step size (e.g., 5 seconds).
Each window contains a sequence of event categories.

Example window sequence:
appInit, resize, toolTip, create

SEQUENTIAL PATTERN MINING
Frequent sequential patterns are extracted using sequential mining techniques.
Patterns represent recurring sequences of events along with their frequency.

Example patterns:
resize → resize (939 occurrences)
readBoundData (1674 occurrences)
appInit → resize (479 occurrences)

TEMPORAL RULE GENERATION
Frequent patterns are converted into temporal rules of the form:

X → Y

Where X is the antecedent sequence and Y is the consequent event.

Each rule is evaluated using:

Frequency (support percentage)
Confidence
Recall
Lift
J-measure
RULE FILTERING
Rules are filtered based on thresholds such as high lift and high confidence to identify strong relationships.
VISUALIZATION
Several visual analysis methods are used:
Correlation matrix of interestingness measures
Pairplot of rule metrics
PCA projection of rules into 2D space
UMAP embedding for non-linear clustering visualization

OUTPUTS

Frequent sequential patterns
Temporal association rules
Ranked rule list
Statistical summaries of rule metrics
PCA and UMAP visualizations

INSIGHTS

Many events show strong self-repetition patterns (e.g., resize → resize)
System-driven events such as readBoundData and toolTip are highly frequent
Several high-confidence rules reflect UI interaction loops
Rule embeddings show clustering of similar behavioral patterns

LIMITATIONS

Self-repeating events can inflate confidence and lift values
Support calculations are approximated from mined patterns rather than raw sequences
Fixed windowing may not accurately represent true user sessions
UMAP may show disconnected graphs due to sparsity in features

FUTURE IMPROVEMENTS

Use session-based segmentation instead of fixed windows
Remove or normalize repeated consecutive events
Compute support directly from raw event sequences
Improve rule quality using PrefixSpan directly
Add anomaly detection for unusual event sequences
Use sequence embeddings for better clustering

TECHNOLOGIES USED
Python
Pandas
PrefixSpan / PyMining
Scikit-learn
UMAP
Matplotlib
Seaborn
