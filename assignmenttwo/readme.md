# UCS654 Predictive Analysis Using Statistics – Assignment 2  
## Learning Probability Density Functions Using Roll-Number-Parameterized Non-Linear Model

---

## 1. Introduction
This assignment focuses on learning an **unknown probability density function (PDF)** using real-world air quality data. A **roll-number-based nonlinear transformation** is applied to the data, and a **Generative Adversarial Network (GAN)** is used to learn the probability distribution of the transformed variable using **samples only**.  
No parametric form of the probability density function is assumed.

---

## 2. Dataset Information
The dataset used is the **India Air Quality Dataset** obtained from [Kaggle](https://www.kaggle.com/datasets/shrutibhargava94/india-air-quality-data).  
From the complete dataset, only the **Nitrogen Dioxide (NO₂)** concentration values are used, represented by the variable `x`.  
Missing and invalid entries in the NO₂ column are removed before further processing.

---

## 3. Methodology
The approach consists of **three main steps**:

### Step 1: Roll-Number-Based Nonlinear Transformation
Each NO₂ value `x` is transformed into a new variable `z` using:

\[
z = x + a_r \cdot \sin(b_r \cdot x)
\]

Where the parameters are calculated using the university roll number `r`:

\[
a_r = 0.5 \times (r \bmod 7)
\]  
\[
b_r = 0.3 \times ((r \bmod 5) + 1)
\]

For **roll number 102317185**, the parameters are:

| Parameter | Value |
|-----------|-------|
| a_r       | 0.5   |
| b_r       | 0.3   |

This ensures each student has a **unique transformed dataset**.

---

### Step 2: Learning the Probability Distribution Using GAN
The transformed variable `z` is assumed to be sampled from an **unknown distribution**.  
A **Generative Adversarial Network (GAN)** is designed and trained using only samples of `z`:

- **Generator:** Takes 10-dimensional Gaussian noise `N(0,1)` and generates fake samples of `z`.  
- **Discriminator:** Distinguishes between real transformed samples and generator outputs.  
- Both networks are trained **adversarially** until the generator produces realistic samples.

---

### Step 3: PDF Approximation from Generator Samples
After training, a **large number of samples** are generated using the trained generator.  
The **probability density function** of `z` is then estimated using **Kernel Density Estimation (KDE)**.  
This estimated PDF represents the learned distribution of the transformed variable.

---

## 4. GAN Architecture

### Generator
| Layer | Description |
|-------|-------------|
| Input | 10-dimensional Gaussian noise |
| Dense | 32 neurons, ReLU activation |
| Dense | 32 neurons, ReLU activation |
| Output | 1 neuron, Tanh activation (scaled output) |

### Discriminator
| Layer | Description |
|-------|-------------|
| Input | 1-dimensional `z` value |
| Dense | 32 neurons, LeakyReLU (0.2) |
| Dense | 16 neurons, LeakyReLU (0.2) |
| Output | 1 neuron, Sigmoid (real/fake probability) |

The architectures are **lightweight** and suitable for learning a **1D probability distribution**.

---

## 5. Results
The trained generator produces samples whose **estimated PDF** closely matches the structure of the transformed data distribution.  
The learned PDF is **smooth** and captures the **dominant characteristics** of the data.

**Plot of learned PDF (GAN vs real KDE):**  
 
<img width="775" height="539" alt="image" src="https://github.com/user-attachments/assets/df58f01d-b5f2-4ef9-bcda-e0c2b017b832" />

---

## 6. Observations

**Mode Coverage:**  
- The generator captures the **dominant peaks** of the transformed distribution without collapsing to a single point.  

**Training Stability:**  
- Training remains stable with minor fluctuations.  
- No severe mode collapse observed.  
- LeakyReLU ensures smooth gradient flow.

**Quality of Generated Distribution:**  
- The generated samples produce a **smooth and realistic PDF**.  
- KDE of generated samples closely matches the **empirical distribution** of transformed data.  

---

## 7. Histogram
- Histogram of transformed variable `z` is generated before GAN training for reference.
<img width="694" height="489" alt="image" src="https://github.com/user-attachments/assets/116e5b79-c9ed-4865-8eb4-da0c7ec70367" />

---

## 8. Conclusion
A **roll-number-based nonlinear transformation** was applied to NO₂ data.  
A **GAN** successfully learned the **unknown probability distribution** of the transformed variable **from data only**, without assuming any analytical form.  
The results demonstrate the effectiveness of GANs in **modeling unknown PDFs** in real-world datasets.

---

## 9. Software and Tools Used
- Google Colab  
- Python  
- NumPy  
- Pandas  
- TensorFlow / Keras  
- Matplotlib  
- SciPy  

---



