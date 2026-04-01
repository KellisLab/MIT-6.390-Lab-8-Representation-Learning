# Lab 8 Assignment Worksheet: Representation Learning & Mantis Map
## MIT 6.390: Introduction to Machine Learning

### Preface to Lab 8

In Part 1 of the lab (the Jupyter Notebooks), you wrote scripts to build and train either an image classifier (CNN on CIFAR-10) or a text classifier (MLP on 20 Newsgroups). 

Instead of treating the entire network as a magical black box that spits out predictions, you explicitly hooked into the layer *right before* the final classes. That layer gives you the high-dimensional internal representation of the data—these are your **Embeddings**. In order to visualize this high-dimensional latent space on a 2D screen, you ran UMAP to generate `coordinate1` and `coordinate2`. You should now have an exported CSV (e.g., `image_analysis_mantis.csv` or `text_analysis_mantis.csv`).

In Part 2 (this document), you will interface with **Mantis**, an agentic, programmable workbench for creating visual and semantic mappings. 

---

### Step 1: Uploading the CSV into Mantis

Because you computed your own embedding vectors using an offline model alongside UMAP, you will bypass Mantis’s default vLLM embedder. This method is called a **Direct Projection**.

1. Navigate to the **Mantis canvas** via the lab links on the MIT course page (`introml.mit.edu/spring26`). If prompted, login with your personal credentials, or use the class-wide dummy login (`6390anon` / `mantis`) if available.
2. Select **Let's Create a New Project**, and set the Project Name (e.g., "6.390 Lab 8 CNN Analysis") and Map Name. 
3. Drag and drop your exported `.csv` file.
   * Mantis parses your column headers automatically. 
4. **Data Typing in Mantis**: Ensure the schema is recognized properly:
   - Make sure your `title` column imports as class `title`.
   - Make sure your `categoric` variable (i.e. ground truth label, like 'dog' or 'alt.atheism') corresponds to a `categoric` tag.
   - Importantly, confirm that `coordinate1` and `coordinate2` are tagged with **override embedding with custom coordinates**. The system will see these and know not to run its own embedding service.
5. In the configuration toggle options underneath the fields:
   * **Reduction Model**: Skip/Ignore (Because you already computed `coordinate1` and `coordinate2` directly, select "Direct Projection (no embedding)").
6. Press the **Create Space** button. 

---

### Step 2: Exploring Cognitive Cartography

Mantis will load a **living map experience**. Your nodes represent the text articles or images you originally fed to the network. Their relative proximity represents how semantically similar the *network* believes those images/items are.

**Answer the following questions as you navigate your new representation visualization:**

1. **Zoom & Isolate Clusters:** 
   Use Mantis to color your points by the `categoric` field. Choose two different colors. Are the classes completely separable, or are there "fuzzy" transition zones between them? Find one example point (image/document) located in a transition zone between two clusters. Briefly describe why the network might find it ambiguous based on its title or content.

2. **Hierarchical "Tree" Viewer:**
   Open the **Tree** element on the dashboard sidebar and sort them according to semantic categories. Which two labels are consistently plotted nearest to each other on the 2D plane based on our offline network’s embedding? (For instance, did 'car' map closely to 'truck'?)

---

### Step 3: Agentic Capabilities & The Notebook Viewer

Mantis provides integrated AI tools that can act out macros via voice, chat, or code. Select a cluster of items—you can select multiple nodes via lasso selection (Bag) or by clicking.

3. Select a neighborhood in the UMAP plot that belongs to the same predicted class. Can you identify any sub-patterns among them? 
4. If you used the Text notebook, run the Mantis **Summarizer** bot on your selected test bag. What does it describe about the overarching theme of this sub-cluster compared to your original ground truth label?

---

### Step 4: Outbedding New Artifacts & Final Reflection

What you’ve created in Part 1 is a mapping from unstructured data space $\rightarrow$ to numerical representation $\rightarrow$ to predicted label. 

Mantis's "Outbedding" features allow creating new artifacts *from latent space positions*. This conceptually proves causality: points mathematically interpolated between a "dog" cluster and a "cat" cluster should, when inverted, produce an item sharing qualities of both.

5. **Reflection Paragraph:** Based on what you just did, describe how the learning progression of your neural network layers relates to "Representation Learning." Contrast the way an early feature map (e.g. edge detection) conceptually differs from this final embedding coordinate plane that groups items by semantic type.

---
### Hand-In Instructions

You do not need to submit the raw CSV file. Please submit:
- Your notebook file (`.ipynb`) showing the successful offline pass training process and loss curve.
- A screenshot of your Mantis Workspace plotting your UMAP embeddings.
- Your numbered answers from Steps 2, 3, and 4.
