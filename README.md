# Papers implementation

I like to read and be inspired by the last reseach papers in Machine Learning, Artificial Intelligence and Deep Learning. 
In this repository, I am implementing the algorithms of those recent papers. 

## Papers Implemented 

### 1. Images Style Transfert

Link:  https://arxiv.org/pdf/1508.06576.pdf

Abstract: *"In ﬁne art,especially painting,humans have mastered the skills to create unique visual experiences through composing a complex interplay between the content and style of an image. [...] Here we introduce an artiﬁcial system based on a Deep Neural Network that creates artistic images of high perceptual quality. The system uses neural representations to separate and recombine content and style of arbitrary images, providing a neural algorithm for the creation of artistic images. Moreover, in light of the striking similarities between performance-optimised artiﬁcial neural networks and biological vision, our work offers a path forward to an algorithmic understanding of how humans create and perceive artistic imagery."* (From the paper)

## Music Generation Papers

In this sections, we are analysing different state of the art approach for generating music using Deep Learning. This problem has numerous challenges: How do we encode the data? How to respect the main musical rules? How to learn the style of a specific artist? How to make a composition sound more human? How to evaluate how good is our generation? How to make our algorithm creative, while still respecting some rules? 

To have a good understanding of the problem and the possible approaches, I am analysing here the more relevant papers in the domain.

### Toward Adaptive Music Generation By Reinforcement Learning of Musical Tension - 2010

**Goal**: to teach the musical agent to choose sequences of musical gesture that will **improve the musical tension perceived** by the listener. **Reinforcement Learning with emotional feedbacks** given by the listener in real time is used. The main goal here is to optimize the emotions felt by the listeners. 

Music is modulated by three parameters: **articulation**, **tempo** and **dynamic**, to implement the perception of musical tension. We want to keep **balance between predictability and surprise**.

### DeepJ: Style Specific Music Generation - 2018

Generative model capable of composing music conditioned on a specific mixture of composer styles. 
Model architecture: **Biaxial LSTM**

For each timestep, at each note, the model produces three outputs: **play probability**, **replay probability** and **dynamics**. There are trained simultaneously using different loss functions: the Binary Cross Entropy for play and replay and the Mean Square Error for dynamics. 

Concerning the evaluation of the model, three approaches are used:
- **User survey**: listen a list of pair of sample and decide **which one produce better sounding music**
- **Style Analysis**: **Survey people with musical background** and ask them to classify music generated as baroque, classical or romantic (Can the model produces stylistically distinct musics)
- **Visualizing style embedding space using tSNE**: analyse the capacity of the model to learn style, composers from similar classical periods tend to cluster together 

### Midinet: A Convolutional Generative Adversarial Network for Symbolic Domain Music Generation - 2017

Uses **CNNs for generating** melody one bar after another in the symbolic domain and uses a **discriminator to learn the distribution** of melodies, which makes it a **GAN**. 

To **emulate creativity** and encorage diverse generation result, a **random noise is used as input** to the generator CNN.

Data representation: The MIDI file is divided into bars. That way, the note events of a MIDI channel can be represented as a HxW real-valued matrix X. *h: number of notes to consider* *w: number of timesteps used in a bar*

### MuseGAN: Multi-track Sequential Generative Adversarial Networks for Symbolic Music Generation and Accompaniment - 2017

In this paper, to cope with the grouping of notes, bars are used instead of notes as the basic compositional unit. Therefore, music is generated one bar after another using **CNN**, which are good for finding local, translation invariant patterns.

An interesting approach in this paper is the evaluation metrics used. Five main characteristics we want our network to have are defined and used to train the network. Then, we can evaluate each of them and assess how well the prediction is doing. The metrics are:
- EB: ration of **empty bars**
- UPC: number of **used pitch classes** per batch (from 0 to 12)
- QN: ratio of **"qualified notes"**. Here, a note longer than three time steps is considered to be qualified. QN shows if the music is overly fragmented.
- DP: (**Drum Pattern**) Ratio of notes in 8- or 16- beat patterns
- TD: (**Tonal Distance**) measure the harmonicity between a pair of tracks. Larger TD implies weaker inter-track harmonic relations.

Concerning the model trained in this paper, it:
- capture some rythmic patterns (good DP)
- contains great amount of fragmented notes 
- produces some noise


### Tuning Recurrent Neural Network with Reinforcement Learning - 2016

The goal here is to use **Reinforcement Learning** to teaches the model to follow certain rules, while still allowing it to retain information learned from data.

For that a couple of **metrics** are defined: 
First those that we want to be low, they are associated with **penalties**:
- **Notes not in key**
- Mean **autocorrelation** (log1 - log2 - log3) : *the goal is to encourage variety, so the model is penalized if the composition is highly correlated with itself*
- Notes **excessively repeated**: *LSTM are prone to repeate the same patterns, Reinforcement Learning is used here to act as a more creative approach*

Then, those that we want to be high, they are associated with **rewards**:
- Compositions **starting with tonic note**
- **Leaps resolved**: *we want to avoid akward interval, so when it is too large, we move back to the opposite direction. In a RL term: leaping two times in the same direction is negatively rewarded*
- Composition with **unique max note**
- Composition with **unique min note** 
- **Note in motif**: *model are rewarded to play motifs: succession of notes representing a short musical "idea"*
- **Note in repeated motif**

Those metrics define a kind of **music theory rule**. The degree of improvement on these metrics is determined by the extend of the **reward** given for the particular behavior. This way, we can give more emphasis on some metrics that are considered more important. For instance, in the model run in this paper, a strong penalty is given each time a note is excessively repeated (-100), while a much smaller reward is given at the end of the composition for a unique extrema note. The choice of the metrics as well as the weights define the shape of the musics we want to create. 

