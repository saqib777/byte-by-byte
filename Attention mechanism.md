# Attention Machanism

Attention is a mechanism that lets a model focus only on the most relevant parts of its input when producing an output. It works using three components: queries (what we're looking for), keys (a searchable representation of each piece of input), and values (the actual content tied to each key). For each query, the model compares it against every key to get similarity scores, turns those scores into weights via softmax, and produces the output as a weighted sum of the values. 

1. Three important variants: self-attention (a sequence attends to itself to build context-aware representations)
2. multi-head attention (multiple independent Q/K/V projections run in parallel so different heads can capture different types of relationships) 
3. soft vs. hard attention (soft uses differentiable, continuous weights; hard uses discrete sampling, which isn't differentiable and needs different training methods like REINFORCE)
