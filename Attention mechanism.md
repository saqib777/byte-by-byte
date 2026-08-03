# Attention Machanism

Attention is a mechanism that lets a model focus only on the most relevant parts of its input when producing an output. It works using three components: queries (what we're looking for), keys (a searchable representation of each piece of input), and values (the actual content tied to each key). For each query, the model compares it against every key to get similarity scores, turns those scores into weights via softmax, and produces the output as a weighted sum of the values. 

1. Three important variants: self-attention (a sequence attends to itself to build context-aware representations)
2. multi-head attention (multiple independent Q/K/V projections run in parallel so different heads can capture different types of relationships) 
3. soft vs. hard attention (soft uses differentiable, continuous weights; hard uses discrete sampling, which isn't differentiable and needs different training methods like REINFORCE)

------

## Working

The working of attention mechanism can be broken down into several key steps

Step 1: Input Encoding: The input sequence is first encoded using an encoder like RNN, LSTM, GRU or Transformer to generate hidden states representing the input context.

Step 2: Query, Key and Value Vectors: Each input is transformed into:

Query (Q): Represents what we’re looking for.
Key (K): Represents what information each input contains.
Value (V): Contains the actual information of each input.
These are linear transformations of the input embeddings.

Step 3: Similarity Computation: The model computes similarity between the query and each key to determine relevance.

<img width="885" height="162" alt="image" src="https://github.com/user-attachments/assets/f3ff4912-4339-4749-b859-8b7c77e8ebb7" />

<img width="657" height="241" alt="image" src="https://github.com/user-attachments/assets/c655a6ce-3aaf-4ced-8654-ed86d7e6c5f5" />


Step 4: Attention Weights Calculation: The similarity scores are passed through a softmax function to convert them into attention weights:

<img width="642" height="80" alt="image" src="https://github.com/user-attachments/assets/8501f5cd-6897-4cf0-a2c8-627c515e500d" />

Step 5: Weighted Sum: The attention weights are used to compute a weighted sum of the value vectors:

c
t
=
∑
i
=
1
T
s
α
(
s
,
i
)
V
i
c 
t
​
 =∑ 
i=1
T 
s
​
 
​
 α(s,i)V 
i
​
 

Here, ​
T
s
T 
s
​
  is the total number of key-value pairs.

Step 6: Context Vector: The context vector 
c
t
c 
t
​
  summarizes the most relevant information from the input sequence and is fed to the decoder.

Step 7: Integration: The decoder uses both its own hidden state and the context vector to generate the next output token.

Attention Mechanism Architecture
Attention is a mechanism used within architectures like encoder-decoder models to improve how information is processed. It works alongside components such as the encoder and decoder by helping the model focus on the most relevant parts of the input.

string_constant_pool_5
Encoder-Decoder with Attention
1. Encoder
The Encoder processes the input sequence like a sentence and converts it into a series of hidden states that represent contextual information about each token.

It typically uses RNNs, LSTMs, GRUs or Transformer-based architectures.
For a sequence of inputs 
x
0
,
x
1
,
x
2
,
x
3
x 
0
​
 ,x 
1
​
 ,x 
2
​
 ,x 
3
​
 ​, the encoder generates hidden representations:
h
0
,
h
1
,
h
2
,
h
3
h 
0
​
 ,h 
1
​
 ,h 
2
​
 ,h 
3
​
 

Each hidden state captures both the current input and information from previous time steps:
h
t
=
f
(
h
t
−
1
,
x
t
)
h 
t
​
 =f(h 
t−1
​
 ,x 
t
​
 )

These hidden states are then passed to the attention layer to calculate which parts of the input are most relevant to the current output step.
2. Attention Mechanism
The Attention component determines how much importance should be given to each encoder hidden state when generating a particular word in the output. Its main goal is to create a context vector 
C
t
C 
t
​
 ​, which captures the most relevant information from the encoder outputs for the current decoding step.

Step 1: Feed-Forward Alignment Function: The decoder’s current hidden state 
S
t
S 
t
​
  and each encoder hidden state 
h
i
h 
i
​
  are combined to compute alignment scores 
e
t
,
i
e 
t,i
​
 :

e
t
,
i
=
g
(
S
t
,
h
i
)
e 
t,i
​
 =g(S 
t
​
 ,h 
i
​
 )

Here,

S
t
S 
t
​
 ​: decoder hidden state at time step t
h
i
h 
i
​
 ​: encoder hidden state for input token i
g
g: feed-forward network that computes alignment score
Typically, g uses a non-linear activation such as tanh, ReLU or sigmoid.

Step 2: Softmax Normalization: The alignment scores are normalized using a softmax function to produce attention weights 
α
t
,
i
α 
t,i
​
 ​ which act like probabilities indicating the importance of each encoder hidden state:

α
t
,
i
=
exp
⁡
(
e
t
,
i
)
∑
k
=
1
T
s
exp
⁡
(
e
t
,
k
)
α 
t,i
​
 = 
∑ 
k=1
T 
s
​
 
​
 exp(e 
t,k
​
 )
exp(e 
t,i
​
 )
​
 

Here,

α
t
,
i
α 
t,i
​
 : attention weight, i.e., how much attention the decoder pays to encoder position i.
T
s
T 
s
​
 ​ is the total number of source tokens.
Step 3: Context Vector Generation: Once attention weights are obtained, they are used to compute a weighted sum of encoder hidden states, forming the context vector 
C
t
C 
t
​
 :

C
t
=
∑
i
=
1
T
s
α
t
,
i
h
i
C 
t
​
 =∑ 
i=1
T 
s
​
 
​
 α 
t,i
​
 h 
i
​
 

Here,

C
t
C 
t
​
 : context vector summarizing encoder outputs
α
t
,
i
α 
t,i
​
 : attention weights
h
i
h 
i
​
 : encoder hidden states
This vector represents the most relevant information from the input sentence needed to predict the next output word.

3. Decoder
The Decoder uses both the context vector 
C
t
C 
t
​
 ​ from the attention layer and its own previous hidden state 
S
t
S 
t
​
  to generate the next output word.

At each decoding step:

The decoder receives 
C
t
C 
t
​
 ​ and the previous predicted word.
It produces a new hidden state 
S
t
+
1
S 
t+1
​
  and predicts the next token.
This process repeats for each word in the target sequence.
Mathematically:

y
t
=
Decoder
(
y
t
−
1
,
S
t
,
C
t
)
y 
t
​
 =Decoder(y 
t−1
​
 ,S 
t
​
 ,C 
t
​
 )

Here,

y
t
−
1
y 
t−1
​
 ​: previously generated token
S
t
S 
t
​
 : decoder hidden state
C
t
C 
t
​
 ​: context vector
This combination enables the model to generate contextually accurate translations hence focusing on the most relevant parts of the source sequence for each predicted word.

Improvement Using Attention Mechanism
Traditional deep learning models like RNNs, LSTMs and CNNs have limitations when handling long or complex dependencies. The attention mechanism enhances their effectiveness as follows:

RNNs/LSTMs: These models compress the entire input into one vector, causing information loss over long sequences. Attention dynamically focuses on the relevant parts, resolving long-term dependency issues.
CNNs: They have fixed receptive fields and attention enables global dependencies, helping capture relationships beyond local patterns.
Seq2Seq Models: Replace single context vectors with multiple dynamic ones, improving translation accuracy.
General Advantage: Helps assign different importance weights to inputs, avoiding equal treatment of all tokens or features.
Transformers: Attention is the core mechanism in Transformers through self-attention, this removes sequential processing limitations of RNNs which improves efficiency and scalability.
Implementation
Let's see the python implementation of Attention Mechanism

Step 1: Define the Attention Class
self.attn: transforms combined decoder hidden state and encoder outputs into an intermediate energy vector
self.v: converts the energy vector into a single score for each time step
hidden.unsqueeze().repeat(): aligns decoder hidden state with all encoder time steps
torch.bmm(v, energy): computes attention scores
softmax: converts scores into attention weights (probabilities)
torch.bmm(...): generates the context vector as a weighted sum of encoder outputs

import torch
import torch.nn as nn
import torch.nn.functional as F


class Attention(nn.Module):
    def __init__(self, hidden_dim):
        super(Attention, self).__init__()
        self.attn = nn.Linear(hidden_dim * 2, hidden_dim)
        self.v = nn.Parameter(torch.rand(hidden_dim))

    def forward(self, hidden, encoder_outputs):
        batch_size = encoder_outputs.shape[0]
        seq_len = encoder_outputs.shape[1]
        hidden = hidden.unsqueeze(1).repeat(1, seq_len, 1)
        energy = torch.tanh(
            self.attn(torch.cat((hidden, encoder_outputs), dim=2)))
        energy = energy.permute(0, 2, 1)
        v = self.v.repeat(batch_size, 1).unsqueeze(1)
        attention_scores = torch.bmm(v, energy).squeeze(1)
        attention_weights = F.softmax(attention_scores, dim=1)
        context = torch.bmm(attention_weights.unsqueeze(1), encoder_outputs)
        return context, attention_weights
        
Step 2: Create Sample Input
torch.manual_seed(0): makes the random tensors deterministic so outputs are repeatable.
encoder_outputs: stands in for the sequence of encoder hidden states.
decoder_hidden: the current decoder hidden state used as the Query to compute attention.

torch.manual_seed(0)

batch_size = 1
seq_len = 4
hidden_dim = 8
encoder_outputs = torch.randn(batch_size, seq_len, hidden_dim)
decoder_hidden = torch.randn(batch_size, hidden_dim)
Step 3: Initialize and Run Attention
1. Attention(hidden_dim): constructs the attention module with the chosen hidden dimension.

2. Calling the module returns:

context: the context vector of shape [batch, 1, hidden_dim].
attn_weights: the attention distribution over the seq_len encoder steps (shape [batch, seq_len]).

attention = Attention(hidden_dim)
context, attn_weights = attention(decoder_hidden, encoder_outputs)
Step 4: Inspect Result
Inspecting attn_weights shows which encoder positions the module focused on (values sum to 1 across the sequence).
context is the weighted sum of encoder outputs which we will pass into the decoder to inform the next prediction.

print("Encoder Outputs:\n", encoder_outputs)
print("\nDecoder Hidden State:\n", decoder_hidden)
print("\nAttention Weights:\n", attn_weights)
print("\nContext Vector:\n", context)
Output:

Screenshot-2025-10-28-145011
Result
You can download source code from here.

Applications
Machine Translation: Focuses on relevant words while generating each output word.
Text Summarization: Selects key information for concise summaries.
Image Captioning: Attends to specific image regions to describe them accurately.
Sentiment Analysis and NER: Highlights important words or entities in text.
Speech Recognition: Focuses on critical audio frames for better transcription.
Advantages
Helps models focus dynamically on the most relevant information.
Solves long-term dependency issues in sequential data.
Improves performance and interpretability in NLP and Vision tasks.
Enables parallel computation (in self-attention) unlike RNNs.
Enhances context understanding in transformer-based models.
Limitations
Computationally expensive for long sequences (especially self-attention).
Requires large memory due to quadratic complexity.
Attention weights can be difficult to interpret in large models.
Needs large datasets for effective training.
