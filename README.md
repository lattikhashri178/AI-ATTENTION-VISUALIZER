#  AI Attention Visualizer

AI Attention Visualizer is a Python and Streamlit-based application that extracts text from a study-notes image, converts the extracted words into numerical embeddings, calculates attention scores, and visualizes the attention given to each word.

The project combines **OCR, word embeddings, and an attention mechanism** into a simple interactive application.

---

##  Features

* Upload study-notes images
* Extract text from images using OCR
* Clean and process extracted words
* Generate word embeddings
* Calculate attention scores
* Display word-level attention using progress bars
* Identify the word with the highest attention score
* Simple and beginner-friendly Streamlit interface

---

##  Technologies Used

* Python
* Streamlit
* NumPy
* Pillow
* Pytesseract
* Tesseract OCR
* Sentence Transformers
* all-MiniLM-L6-v2

---

##  Project Structure

```text
AI-Attention-Visualizer/
│
├── app.py
├── attention.py
├── embedding.py
├── ocr.py
├── requirement.txt
└── README.md
```

### File Description

| File              | Description                         |
| ----------------- | ----------------------------------- |
| `app.py`          | Main Streamlit application          |
| `attention.py`    | Calculates attention scores         |
| `embedding.py`    | Generates word embeddings           |
| `ocr.py`          | Extracts text from images using OCR |
| `requirement.txt` | Contains required Python packages   |
| `README.md`       | Project documentation               |

---

##  Project Workflow

```text
        Upload Image
             ↓
          OCR
             ↓
       Extract Text
             ↓
      Process Words
             ↓
    Generate Embeddings
             ↓
    Calculate Attention
             ↓
     Normalize Scores
             ↓
   Display Word Attention
             ↓
 Find Highest Attention Word
```

---

##  1. Upload Image
<img width="1067" height="1600" alt="1" src="https://github.com/user-attachments/assets/7e07ea56-ac6e-479b-8b91-3c1e8bb372f8" />
<img width="995" height="783" alt="2" src="https://github.com/user-attachments/assets/71694b3a-a8e2-4538-a2dc-c810ca6f7a3b" />
<img width="1001" height="747" alt="3" src="https://github.com/user-attachments/assets/6f8fbb7b-f8a0-4203-8f00-248e68c2bf28" />
<img width="942" height="800" alt="4" src="https://github.com/user-attachments/assets/309babb0-a7a8-475b-a287-7944a278cd8a" />
<img width="852" height="612" alt="5" src="https://github.com/user-attachments/assets/8e24dcc6-edc6-42df-baa2-f398aa6a8039" />
<img width="982" height="365" alt="6" src="https://github.com/user-attachments/assets/8401a475-97ff-4b67-8a64-42f0a1a5535e" />






##  2. Text Extraction Using OCR

The project uses **Tesseract OCR** to extract text from the uploaded image.

The `ocr.py` file uses the `pytesseract` library.

```python
def extract_text(image):
    return pytesseract.image_to_string(image)
```

Tesseract OCR is configured using:

```text
C:\Program Files\Tesseract-OCR\tesseract.exe
```

If Tesseract is installed in a different location, the path in `ocr.py` should be changed.

---

##  3. Word Processing

After extracting the text, the application splits the text into individual words.

Punctuation is removed from the words.

The application removes words with fewer than 3 characters.

It also limits the processed words to a maximum of 20 words.

Example:

```text
Original Text:
Artificial intelligence is changing technology.

Processed Words:
Artificial
intelligence
changing
technology
```

---

##  4. Generate Word Embeddings

The project uses the Sentence Transformer model:

```text
all-MiniLM-L6-v2
```

The model is loaded using:

```python
model = SentenceTransformer("all-MiniLM-L6-v2")
```

The words are converted into numerical vector representations called **embeddings**.

```python
def create_embeddings(words):
    embeddings = model.encode(words)
    return embeddings
```

These embeddings are then passed to the attention calculation module.

---

##  5. Attention Calculation

The project implements a simple attention mechanism using NumPy.

The embedding matrix is used to generate:

* Query (Q)
* Key (K)
* Value (V)

The calculations are:

```text
Q = X × WQ
K = X × WK
V = X × WV
```

The attention score is calculated using:

```text
Q × Kᵀ
```

The score is then scaled using:

```text
Score / √dk
```

The project uses:

```python
d_k = 64
```

Softmax is then applied to calculate attention weights.

---

##  6. Attention Scores

After calculating the attention weights, the project calculates the average attention score for each word.

```python
word_scores = attention_weights.mean(axis=0)
```

The scores are normalized before displaying them:

```python
display_scores = scores / scores.max()
```

This allows the attention values to be displayed using Streamlit progress bars.

---

##  7. Word Attention Visualization

The application displays every processed word along with its attention score.

Example:

```text
Artificial       ████████████
Intelligence     █████████████████
Technology       ████████
Learning         ██████████
```

The progress bar represents the relative attention score of each word.

---

##  8. Highest Attention Word

The application identifies the word with the highest attention score.

```python
top_index = np.argmax(scores)
top_word = words[top_index]
```

The result is displayed in the application:

```text
Highest Attention Word: Intelligence
```

---

#  Installation

## Step 1: Clone the Repository

```bash
git clone https://github.com/your-username/AI-Attention-Visualizer.git
```

Then move into the project folder:

```bash
cd AI-Attention-Visualizer
```

---

## Step 2: Install Python Packages

Install all required packages using:

```bash
pip install -r requirement.txt
```

The project requires:

```text
streamlit
numpy
pillow
pytesseract
sentence-transformers
```

---

## Step 3: Install Tesseract OCR

Tesseract OCR is required for extracting text from images.

After installing Tesseract, make sure the executable path matches the path in `ocr.py`.

Current path:

```text
C:\Program Files\Tesseract-OCR\tesseract.exe
```

If your installation is located somewhere else, update the path in:

```text
ocr.py
```

---

#  Run the Application

Run the Streamlit application using:

```bash
python -m streamlit run app.py
```

After running the command, Streamlit will provide a local URL.

Open that URL in your web browser.

---

#  How to Use

### Step 1

Run the Streamlit application.

### Step 2

Upload a study-notes image.

### Step 3

The application extracts text from the image using OCR.

### Step 4

The extracted text is cleaned and converted into individual words.

### Step 5

The words are converted into embeddings using Sentence Transformers.

### Step 6

The attention mechanism calculates attention scores.

### Step 7

The attention scores are displayed using progress bars.

### Step 8

The application displays the word with the highest attention score.

---

# 📦 Requirements

The `requirement.txt` file contains:

```text
streamlit
numpy
pillow
pytesseract
sentence-transformers
```

---

# 🧩 Main Concepts

## OCR

OCR stands for **Optical Character Recognition**.

OCR converts text present in an image into machine-readable text.

In this project, Tesseract OCR is used to extract text from study notes.

---

## Word Embeddings

Word embeddings represent words as numerical vectors.

This project uses the Sentence Transformer model:

```text
all-MiniLM-L6-v2
```

The embeddings are then used as input to the attention calculation.

---

## Attention Mechanism

Attention is a mechanism used in AI and Natural Language Processing to calculate relationships between different parts of input data.

This project demonstrates a simplified attention mechanism using:

```text
Query
Key
Value
Scaling
Softmax
Attention Weights
```

---

#  Project Objective

The main objective of the project is to demonstrate how different AI and NLP techniques can be combined in a single application.

The application performs the following tasks:

1. Reads text from an image.
2. Extracts the text using OCR.
3. Processes the extracted words.
4. Converts words into embeddings.
5. Calculates attention scores.
6. Visualizes the attention scores.
7. Identifies the highest-attention word.

---

#  Attention Formula

The project follows the basic scaled attention calculation:

```text
Attention(Q, K, V)
=
softmax(QKᵀ / √dk)V
```

The implementation first calculates:

```text
Q = XWQ
K = XWK
V = XWV
```

Then:

```text
Scores = QKᵀ
```

The scores are scaled:

```text
Scaled Scores = Scores / √dk
```

Finally, softmax is applied to obtain attention weights.

---

# Future Enhancements

The project can be further improved by adding:

* Better image preprocessing
* Improved OCR accuracy
* Handwritten-text recognition
* Heatmap-based attention visualization
* Interactive attention visualization
* Sentence-level attention
* Transformer-based attention visualization
* PDF support
* Multiple image support
* Downloadable attention reports
* Improved Streamlit user interface
* More advanced NLP models

---

#  Example Workflow

```text
Study Notes Image
       ↓
     Tesseract
       ↓
  Extracted Text
       ↓
  Word Processing
       ↓
Sentence Transformer
       ↓
 Word Embeddings
       ↓
 Attention Mechanism
       ↓
 Attention Scores
       ↓
Word Visualization
       ↓
Highest Attention Word
```

---

#  Project Modules

## `app.py`

This is the main application file.

It:

* Creates the Streamlit interface
* Accepts image uploads
* Displays the uploaded image
* Calls the OCR module
* Processes words
* Calls the embedding module
* Calls the attention module
* Displays attention scores
* Finds the highest-attention word

---

## `ocr.py`

This module performs OCR.

It uses:

```text
pytesseract
```

to extract text from the uploaded image.

---

## `embedding.py`

This module creates embeddings using:

```text
SentenceTransformer
```

and the:

```text
all-MiniLM-L6-v2
```

model.

---

## `attention.py`

This module calculates the attention scores.

It implements:

```text
Query
Key
Value
Scaled Scores
Softmax
Attention Weights
Word Scores
```

using NumPy.

