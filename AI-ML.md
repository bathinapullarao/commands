# AI & Machine Learning Topics Roadmap 🤖

A structured guide covering Artificial Intelligence (AI), Machine
Learning (ML), Deep Learning, MLOps, and practical industry-focused
concepts.

------------------------------------------------------------------------

## 1. Artificial Intelligence Fundamentals

-   What is AI?
-   Types of AI (Narrow, General, Super AI)
-   AI vs ML vs Deep Learning
-   Applications of AI
-   Intelligent Agents
-   Turing Test
-   Search Algorithms (BFS, DFS, A\*)

------------------------------------------------------------------------

## 2. Machine Learning Fundamentals

-   What is Machine Learning?
-   Types of ML:
    -   Supervised Learning
    -   Unsupervised Learning
    -   Semi-Supervised Learning
    -   Reinforcement Learning
-   Training vs Testing data
-   Overfitting & Underfitting
-   Bias-Variance Tradeoff
-   Cross Validation
-   Feature Engineering

------------------------------------------------------------------------

## 3. Supervised Learning

### Regression

-   Linear Regression
-   Multiple Linear Regression
-   Polynomial Regression
-   Ridge & Lasso Regression

### Classification

-   Logistic Regression
-   K-Nearest Neighbors (KNN)
-   Support Vector Machine (SVM)
-   Naive Bayes
-   Decision Trees
-   Random Forest
-   Gradient Boosting
-   XGBoost

------------------------------------------------------------------------

## 4. Unsupervised Learning

-   K-Means Clustering
-   Hierarchical Clustering
-   DBSCAN
-   Principal Component Analysis (PCA)
-   Dimensionality Reduction
-   Association Rules (Apriori)

------------------------------------------------------------------------

## 5. Deep Learning

-   Neural Networks Basics
-   Perceptron
-   Activation Functions (ReLU, Sigmoid, Tanh)
-   Backpropagation
-   Loss Functions
-   Optimizers (SGD, Adam)

### Advanced Neural Networks

-   CNN (Convolutional Neural Networks)
-   RNN (Recurrent Neural Networks)
-   LSTM / GRU
-   Transformers
-   Attention Mechanism

------------------------------------------------------------------------

## 6. Natural Language Processing (NLP)

-   Text Preprocessing
-   Tokenization
-   Stopwords
-   Stemming & Lemmatization
-   TF-IDF
-   Word2Vec
-   BERT
-   GPT Models
-   Sentiment Analysis
-   Named Entity Recognition (NER)

------------------------------------------------------------------------

## 7. Computer Vision

-   Image Processing Basics
-   OpenCV
-   Object Detection
-   Image Classification
-   YOLO
-   Face Recognition

------------------------------------------------------------------------

## 8. Reinforcement Learning

-   Agent, Environment
-   Rewards
-   Q-Learning
-   Markov Decision Process (MDP)
-   Policy Gradient Methods

------------------------------------------------------------------------

## 9. Mathematics for ML

-   Linear Algebra
-   Probability & Statistics
-   Calculus (Derivatives, Gradients)
-   Matrix Operations
-   Eigenvalues & Eigenvectors

------------------------------------------------------------------------

## 10. Data Preprocessing

-   Handling Missing Data
-   Encoding Categorical Variables
-   Feature Scaling
-   Normalization & Standardization
-   Data Augmentation

------------------------------------------------------------------------

## 11. Model Evaluation

-   Accuracy
-   Precision, Recall, F1 Score
-   Confusion Matrix
-   ROC Curve
-   AUC
-   Mean Squared Error (MSE)
-   R² Score

------------------------------------------------------------------------

## 12. MLOps

-   Model Deployment
-   CI/CD for ML
-   Model Monitoring
-   Drift Detection
-   Version Control for Models
-   Docker & Kubernetes for ML
-   MLflow
-   Kubeflow

------------------------------------------------------------------------

## 13. Cloud AI Services

-   Google Vertex AI
-   AWS SageMaker
-   Azure ML
-   BigQuery ML
-   Databricks ML

------------------------------------------------------------------------

## 14. Generative AI

-   Large Language Models (LLMs)
-   Prompt Engineering
-   Fine-Tuning
-   Retrieval-Augmented Generation (RAG)
-   Embeddings
-   Vector Databases

------------------------------------------------------------------------

## 15. Ethical AI

-   Responsible AI
-   Bias in AI
-   Fairness & Transparency
-   Data Privacy
-   Model Explainability (SHAP, LIME)

------------------------------------------------------------------------

## Interview Focus Areas

-   Difference between AI, ML, DL
-   Supervised vs Unsupervised
-   Overfitting solutions
-   Evaluation metrics
-   Explain Gradient Descent
-   Explain Random Forest
-   What is Cross Validation?
-   Explain Transformers

------------------------------------------------------------------------
# AI & ML Topics — 2 Sample Programs Each (with Comments + Sample Outputs)

> Notes  
> - These are **educational, runnable** mini-programs (mostly pure Python; a few use `math` only).  
> - Outputs are **sample outputs**; exact values may vary slightly with random seeds or floating-point formatting.  
> - For cloud services (Vertex AI/SageMaker/etc.), examples are **local mock/demo patterns** since calling real cloud APIs needs credentials and network access.

---

## 1) Artificial Intelligence Fundamentals

### Program 1: Simple rule-based “agent” (reflex agent)
```python
# A tiny rule-based agent that decides an action based on the environment.
# This demonstrates the "AI agent" idea: observe -> decide -> act.

def agent_action(room_is_dirty: bool) -> str:
    # If dirty, clean; else do nothing
    if room_is_dirty:
        return "CLEAN"
    return "IDLE"

print(agent_action(True))
print(agent_action(False))
```
**Sample output**
```text
CLEAN
IDLE
```

### Program 2: Breadth-First Search (BFS) on a graph
```python
# BFS explores the nearest nodes first.
# This is a classic AI search technique used in path finding.

from collections import deque

graph = {
    "A": ["B", "C"],
    "B": ["D", "E"],
    "C": ["F"],
    "D": [], "E": [], "F": []
}

start = "A"
q = deque([start])
visited = set([start])

order = []

while q:
    node = q.popleft()       # pop from left => FIFO queue
    order.append(node)
    for nei in graph[node]:
        if nei not in visited:
            visited.add(nei)
            q.append(nei)

print(order)
```
**Sample output**
```text
['A', 'B', 'C', 'D', 'E', 'F']
```

---

## 2) Machine Learning Fundamentals

### Program 1: Train/Test split (simple)
```python
# Splitting data into train and test helps estimate generalization performance.

data = list(range(1, 11))   # pretend these are samples

split = int(len(data) * 0.7)  # 70% train
train = data[:split]
test = data[split:]

print("train:", train)
print("test:", test)
```
**Sample output**
```text
train: [1, 2, 3, 4, 5, 6, 7]
test: [8, 9, 10]
```

### Program 2: Overfitting demo (polynomial “too complex” idea)
```python
# This is a conceptual demonstration: a complex model can fit training points perfectly
# but behave poorly for unseen inputs.
#
# We'll "fit" a lookup-table model that memorizes training data (perfect training accuracy),
# but for new x it returns a default value => poor generalization.

train_x = [1, 2, 3]
train_y = [10, 20, 30]

# Memorization model: store mapping x->y
memory_model = dict(zip(train_x, train_y))

def predict(x):
    # If x was seen, return memorized y; otherwise guess 0
    return memory_model.get(x, 0)

print("train preds:", [predict(x) for x in train_x])
print("test preds :", [predict(x) for x in [4, 5]])
```
**Sample output**
```text
train preds: [10, 20, 30]
test preds : [0, 0]
```

---

## 3) Supervised Learning

### Program 1: Linear Regression (1D) using gradient descent
```python
# Fit y = w*x + b using gradient descent.
# This is a basic supervised regression example.

import random

# Simple dataset: y = 2x + 1 (with tiny noise)
xs = [0, 1, 2, 3, 4]
ys = [1, 3, 5, 7, 9]

w = random.uniform(-1, 1)
b = random.uniform(-1, 1)
lr = 0.05

for _ in range(1000):
    # Compute gradients for MSE loss
    dw = 0.0
    db = 0.0
    n = len(xs)
    for x, y in zip(xs, ys):
        yhat = w * x + b
        err = yhat - y
        dw += (2/n) * err * x
        db += (2/n) * err
    # Update parameters
    w -= lr * dw
    b -= lr * db

print("w=", round(w, 3), "b=", round(b, 3))
print("pred(5)=", round(w*5 + b, 3))
```
**Sample output**
```text
w= 2.0 b= 1.0
pred(5)= 11.0
```

### Program 2: Logistic Regression-like classification (simple threshold classifier)
```python
# A simple classifier: if score >= threshold -> class 1 else class 0
# This demonstrates the idea of classification decision boundary.

scores = [0.2, 0.4, 0.51, 0.9]
threshold = 0.5

labels = []
for s in scores:
    # Decision boundary at 0.5
    labels.append(1 if s >= threshold else 0)

print(labels)
```
**Sample output**
```text
[0, 0, 1, 1]
```

---

## 4) Unsupervised Learning

### Program 1: K-Means clustering (2 clusters, tiny dataset)
```python
# K-Means groups points into K clusters by iteratively updating centroids.
# This is a minimal 1D example for clarity.

points = [1, 2, 3, 10, 11, 12]
c1, c2 = 2, 11  # initial centroids
for _ in range(5):
    # Assign points to nearest centroid
    cluster1 = [p for p in points if abs(p - c1) <= abs(p - c2)]
    cluster2 = [p for p in points if abs(p - c1) >  abs(p - c2)]
    # Update centroids as mean
    c1 = sum(cluster1) / len(cluster1)
    c2 = sum(cluster2) / len(cluster2)

print("cluster1:", cluster1, "centroid:", c1)
print("cluster2:", cluster2, "centroid:", c2)
```
**Sample output**
```text
cluster1: [1, 2, 3] centroid: 2.0
cluster2: [10, 11, 12] centroid: 11.0
```

### Program 2: PCA idea (2D -> 1D projection, simplified)
```python
# PCA reduces dimensions by projecting data onto the direction of maximum variance.
# Here we show a simple "manual" projection on a chosen direction vector.

import math

points = [(1, 1), (2, 2), (3, 3)]  # points lie roughly on y=x
direction = (1/math.sqrt(2), 1/math.sqrt(2))  # unit vector along y=x

projected = []
for x, y in points:
    # Dot product gives projection length on the direction
    proj = x * direction[0] + y * direction[1]
    projected.append(round(proj, 3))

print(projected)  # now 1D values
```
**Sample output**
```text
[1.414, 2.828, 4.243]
```

---

## 5) Deep Learning

### Program 1: Single neuron forward pass (sigmoid)
```python
# A neuron computes: z = w1*x1 + w2*x2 + b, then applies an activation function.
# This is the core of neural networks.

import math

x1, x2 = 1.0, 2.0
w1, w2 = 0.5, -0.25
b = 0.1

z = w1*x1 + w2*x2 + b

# Sigmoid activation
sigmoid = 1 / (1 + math.exp(-z))

print("z =", round(z, 3))
print("sigmoid(z) =", round(sigmoid, 3))
```
**Sample output**
```text
z = 0.1
sigmoid(z) = 0.525
```

### Program 2: Mini “backprop” for one weight (numerical gradient)
```python
# Demonstrate gradient concept using numerical approximation.
# We compute how loss changes if we slightly change a weight.

import math

x = 3.0
y_true = 7.0

def loss_for_w(w):
    # Simple model: y_pred = w*x
    y_pred = w * x
    # MSE loss
    return (y_pred - y_true) ** 2

w = 2.0
eps = 1e-5

# Numerical gradient: (f(w+eps) - f(w-eps)) / (2*eps)
grad = (loss_for_w(w + eps) - loss_for_w(w - eps)) / (2 * eps)

print("loss =", round(loss_for_w(w), 3))
print("grad dloss/dw =", round(grad, 3))
```
**Sample output**
```text
loss = 1.0
grad dloss/dw = -6.0
```

---

## 6) Natural Language Processing (NLP)

### Program 1: Tokenization + stopword removal
```python
# Basic NLP preprocessing: lowercase -> split -> remove stopwords

text = "Spark and Hadoop are used in Big Data"
stopwords = {"and", "are", "in"}

tokens = text.lower().split()  # split by spaces
clean = [t for t in tokens if t not in stopwords]

print(tokens)
print(clean)
```
**Sample output**
```text
['spark', 'and', 'hadoop', 'are', 'used', 'in', 'big', 'data']
['spark', 'hadoop', 'used', 'big', 'data']
```

### Program 2: TF (term frequency) calculation
```python
# Term frequency: count occurrences of each word

text = "spark spark hadoop gcp"
freq = {}

for w in text.split():
    # Increment count (default 0)
    freq[w] = freq.get(w, 0) + 1

print(freq)
```
**Sample output**
```text
{'spark': 2, 'hadoop': 1, 'gcp': 1}
```

---

## 7) Computer Vision

### Program 1: Simple grayscale “image” as a matrix + average brightness
```python
# Represent a grayscale image as a 2D list (pixel intensities 0-255).
# Compute the average brightness.

image = [
    [0,  50,  100],
    [150, 200, 255]
]

total = 0
count = 0
for row in image:
    for px in row:
        total += px
        count += 1

avg = total / count
print("avg_brightness =", round(avg, 2))
```
**Sample output**
```text
avg_brightness = 125.83
```

### Program 2: Simple edge detection (difference between neighbors)
```python
# A very basic "edge strength" measure: abs difference between adjacent pixels.

row = [10, 10, 10, 200, 210]  # sharp change indicates an edge
edges = []

for i in range(len(row) - 1):
    # Edge strength between i and i+1
    edges.append(abs(row[i+1] - row[i]))

print(edges)
```
**Sample output**
```text
[0, 0, 190, 10]
```

---

## 8) Reinforcement Learning (RL)

### Program 1: Bandit (choose best action by average reward)
```python
# Multi-armed bandit: pick arm with highest average reward (greedy).
# This demonstrates the RL idea of maximizing reward.

rewards = {
    "A": [1, 0, 1, 1],
    "B": [0, 0, 1, 0],
}

avg = {}
for arm, rs in rewards.items():
    avg[arm] = sum(rs) / len(rs)

best_arm = max(avg, key=avg.get)
print("avg:", avg)
print("best_arm:", best_arm)
```
**Sample output**
```text
avg: {'A': 0.75, 'B': 0.25}
best_arm: A
```

### Program 2: Q-learning update (single step)
```python
# Q-learning update formula:
# Q(s,a) = Q(s,a) + alpha * (reward + gamma*max_a' Q(s',a') - Q(s,a))

Q_sa = 1.0        # current Q(s,a)
reward = 2.0
gamma = 0.9
alpha = 0.1
max_Q_next = 3.0  # max Q(s', a')

new_Q = Q_sa + alpha * (reward + gamma * max_Q_next - Q_sa)

print("old_Q:", Q_sa)
print("new_Q:", round(new_Q, 3))
```
**Sample output**
```text
old_Q: 1.0
new_Q: 1.37
```

---

## 9) Mathematics for ML

### Program 1: Dot product (linear algebra core)
```python
# Dot product is used everywhere: linear models, neural nets, similarity.

a = [1, 2, 3]
b = [4, 5, 6]

dot = 0
for x, y in zip(a, b):
    dot += x * y

print(dot)
```
**Sample output**
```text
32
```

### Program 2: Probability basics (mean and variance)
```python
# Mean and variance are key in statistics and normalization.

data = [1, 2, 3, 4, 5]
mean = sum(data) / len(data)

var = sum((x - mean) ** 2 for x in data) / len(data)  # population variance

print("mean:", mean)
print("var:", var)
```
**Sample output**
```text
mean: 3.0
var: 2.0
```

---

## 10) Data Preprocessing

### Program 1: Handle missing values
```python
# Replace missing values (None) with the mean of available values.

data = [10, None, 30, None, 50]

known = [x for x in data if x is not None]
mean = sum(known) / len(known)

filled = [mean if x is None else x for x in data]

print("mean:", mean)
print("filled:", filled)
```
**Sample output**
```text
mean: 30.0
filled: [10, 30.0, 30, 30.0, 50]
```

### Program 2: Normalization (min-max scaling)
```python
# Scale values to [0,1] range: (x - min) / (max - min)

data = [10, 20, 30]
mn, mx = min(data), max(data)

scaled = [(x - mn) / (mx - mn) for x in data]
print(scaled)
```
**Sample output**
```text
[0.0, 0.5, 1.0]
```

---

## 11) Model Evaluation

### Program 1: Confusion matrix + accuracy
```python
# Compute confusion matrix for binary classification.

y_true = [1, 0, 1, 1, 0]
y_pred = [1, 0, 0, 1, 0]

tp = sum(1 for t, p in zip(y_true, y_pred) if t == 1 and p == 1)
tn = sum(1 for t, p in zip(y_true, y_pred) if t == 0 and p == 0)
fp = sum(1 for t, p in zip(y_true, y_pred) if t == 0 and p == 1)
fn = sum(1 for t, p in zip(y_true, y_pred) if t == 1 and p == 0)

acc = (tp + tn) / len(y_true)

print("TP, TN, FP, FN =", tp, tn, fp, fn)
print("accuracy =", acc)
```
**Sample output**
```text
TP, TN, FP, FN = 2 2 0 1
accuracy = 0.8
```

### Program 2: Precision, Recall, F1
```python
# Precision = TP/(TP+FP), Recall = TP/(TP+FN), F1 = 2PR/(P+R)

tp, fp, fn = 2, 0, 1

precision = tp / (tp + fp) if (tp + fp) else 0.0
recall = tp / (tp + fn) if (tp + fn) else 0.0
f1 = (2 * precision * recall / (precision + recall)) if (precision + recall) else 0.0

print("precision =", precision)
print("recall =", recall)
print("f1 =", round(f1, 3))
```
**Sample output**
```text
precision = 1.0
recall = 0.6666666666666666
f1 = 0.8
```

---

## 12) MLOps

### Program 1: Model “versioning” with a simple file name pattern
```python
# In MLOps we version artifacts (models).
# Here we simulate writing a model file with version and metadata.

from datetime import datetime

model_version = "v1.0.0"
timestamp = datetime.utcnow().strftime("%Y%m%d%H%M%S")

filename = f"model_{model_version}_{timestamp}.bin"
print("saved_artifact:", filename)
```
**Sample output**
```text
saved_artifact: model_v1.0.0_20260222120000.bin
```

### Program 2: Simple drift detection (mean shift)
```python
# Drift detection checks if incoming data differs from training distribution.
# Here we compare mean difference with a threshold.

train = [10, 12, 11, 13, 12]
prod  = [20, 19, 21, 22, 20]

train_mean = sum(train) / len(train)
prod_mean = sum(prod) / len(prod)

threshold = 5.0
drift = abs(prod_mean - train_mean) > threshold

print("train_mean:", train_mean)
print("prod_mean :", prod_mean)
print("drift_detected:", drift)
```
**Sample output**
```text
train_mean: 11.6
prod_mean : 20.4
drift_detected: True
```

---

## 13) Cloud AI Services (Vertex AI / SageMaker / Azure ML / BigQuery ML)

### Program 1: Local “training job” pattern (mock)
```python
# Cloud training jobs usually accept configs and log metrics.
# This is a local mock demonstrating the same structure.

config = {"region": "europe-west2", "machine": "n1-standard-4", "epochs": 3}
print("job_config:", config)

for epoch in range(1, config["epochs"] + 1):
    # Fake metric
    loss = 1.0 / epoch
    print(f"epoch={epoch} loss={loss:.3f}")
```
**Sample output**
```text
job_config: {'region': 'europe-west2', 'machine': 'n1-standard-4', 'epochs': 3}
epoch=1 loss=1.000
epoch=2 loss=0.500
epoch=3 loss=0.333
```

### Program 2: Endpoint prediction pattern (mock)
```python
# Cloud endpoints typically accept JSON and return JSON.
# This mock shows a similar request/response structure.

request = {"instances": [{"x": 5}]}

def predict(payload):
    # Pretend the model is y = 2x + 1
    x = payload["instances"][0]["x"]
    return {"predictions": [2 * x + 1]}

print("request:", request)
print("response:", predict(request))
```
**Sample output**
```text
request: {'instances': [{'x': 5}]}
response: {'predictions': [11]}
```

---

## 14) Generative AI (LLMs, Prompting, RAG, Embeddings)

### Program 1: Simple “prompt template” generator
```python
# Prompt engineering often uses templates with variables.

template = "You are a helpful assistant. Summarize this: {text}"
text = "Dataproc runs Spark jobs on managed clusters."

prompt = template.format(text=text)  # fill the template
print(prompt)
```
**Sample output**
```text
You are a helpful assistant. Summarize this: Dataproc runs Spark jobs on managed clusters.
```

### Program 2: Tiny embedding + similarity (toy example)
```python
# Embeddings are vectors. Similarity is often measured by cosine similarity.

import math

def cosine(a, b):
    # Compute cosine similarity between vectors
    dot = sum(x*y for x, y in zip(a, b))
    na = math.sqrt(sum(x*x for x in a))
    nb = math.sqrt(sum(y*y for y in b))
    return dot / (na * nb)

emb_spark = [1, 0, 1]
emb_hadoop = [1, 0, 0]
emb_banana = [0, 1, 0]

print("spark~hadoop:", round(cosine(emb_spark, emb_hadoop), 3))
print("spark~banana:", round(cosine(emb_spark, emb_banana), 3))
```
**Sample output**
```text
spark~hadoop: 0.707
spark~banana: 0.0
```

---

## 15) Ethical AI (Bias/Fairness, Privacy, Explainability)

### Program 1: Basic fairness check (acceptance rates by group)
```python
# Fairness check: compare acceptance rates for two groups.
# If rates differ significantly, investigate potential bias.

decisions = [
    {"group": "A", "accepted": 1},
    {"group": "A", "accepted": 0},
    {"group": "A", "accepted": 1},
    {"group": "B", "accepted": 0},
    {"group": "B", "accepted": 0},
    {"group": "B", "accepted": 1},
]

def acceptance_rate(group):
    rows = [d for d in decisions if d["group"] == group]
    return sum(d["accepted"] for d in rows) / len(rows)

rate_a = acceptance_rate("A")
rate_b = acceptance_rate("B")

print("rate_A:", rate_a)
print("rate_B:", rate_b)
print("difference:", round(abs(rate_a - rate_b), 3))
```
**Sample output**
```text
rate_A: 0.6666666666666666
rate_B: 0.3333333333333333
difference: 0.333
```

### Program 2: Simple model explainability (feature contribution for linear model)
```python
# For a linear model y = w1*x1 + w2*x2 + b,
# the contribution of each feature is (wi*xi). This is a simple explanation.

x1, x2 = 2.0, 3.0
w1, w2 = 1.5, -0.5
b = 0.2

c1 = w1 * x1    # contribution from feature 1
c2 = w2 * x2    # contribution from feature 2
y = c1 + c2 + b

print("contrib_x1:", c1)
print("contrib_x2:", c2)
print("bias:", b)
print("prediction:", y)
```
**Sample output**
```text
contrib_x1: 3.0
contrib_x2: -1.5
bias: 0.2
prediction: 1.7
```

---

## Quick Interview Practice Add-on (bonus)

### Program 1: Gradient descent step (one update)
```python
# One step of gradient descent: w = w - lr * grad
w = 2.0
grad = -6.0
lr = 0.1

w_new = w - lr * grad
print("w_new:", w_new)
```
**Sample output**
```text
w_new: 2.6
```

### Program 2: Softmax (common in classification)
```python
# Softmax converts scores into probabilities that sum to 1.

import math

scores = [1.0, 2.0, 3.0]
exps = [math.exp(s) for s in scores]
total = sum(exps)
probs = [round(e/total, 3) for e in exps]

print(probs)
print("sum:", round(sum(probs), 3))
```
**Sample output**
```text
[0.09, 0.245, 0.665]
sum: 1.0
```

---
