# Papers implementation

I like to read and be inspired by the last reseach papers in Machine Learning, Artificial Intelligence and Deep Learning. 
In this repository, I am implementing the algorithms of those recent papers. 

## Papers Implemented 

### 1. Images Style Transfert

Link:  https://arxiv.org/pdf/1508.06576.pdf

Abstract: *"In ﬁne art,especially painting,humans have mastered the skills to create unique visual experiences through composing a complex interplay between the content and style of an image. [...] Here we introduce an artiﬁcial system based on a Deep Neural Network that creates artistic images of high perceptual quality. The system uses neural representations to separate and recombine content and style of arbitrary images, providing a neural algorithm for the creation of artistic images. Moreover, in light of the striking similarities between performance-optimised artiﬁcial neural networks and biological vision, our work offers a path forward to an algorithmic understanding of how humans create and perceive artistic imagery."* (From the paper)

## Music Style Transfer Papers

In this sections, we are analysing different state of the art approach for generating music using Deep Learning. This problem has numerous challenges: How do we encode the data? How to respect the main musical rules? How to learn the style of a specific artist? How to make a composition sound more human? How to evaluate how good is our generation? how to make our algorithm creative, while still respecting some rules? 

To have a good understanding of the problem and the possible approaches, I am analysing here the more relevant papers in the domain.

### Toward Adaptive Music Generation By Reinforcement Learning of Musical Tension

### DeepJ: Style Specific Music Generation

### Midinet: A Convolutional Generative Adversarial Network for Symbolic Domain Music Generation

Uses **CNNs for generating** melody one bar after another in the symbolic domain and uses a **discriminator to learn the distribution** of melodies, which makes it a **GAN**. 

To **emulate creativity** and encorage diverse generation result, a **random noise is used as input** to the generator CNN.

Data representation: The MIDI file is divided into bars. That way, the note events of a MIDI channel can be represented as a HxW real-valued matrix X. *h: number of notes to consider* *w: number of timesteps used in a bar*

### MuseGAN: Multi-track Sequential Generative Adversarial Networks for Symbolic Music Generation and Accompaniment

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


### Tuning Recurrent Neural Network with Reinforcement Learning


