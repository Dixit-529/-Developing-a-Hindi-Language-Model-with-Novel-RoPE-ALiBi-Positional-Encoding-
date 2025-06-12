# -Developing-a-Hindi-Language-Model-with-Novel-RoPE-ALiBi-Positional-Encoding-

Project completed in 5 stages:
1. Data Collection
2. Data Pre-Processing
3. Tokenizer
4. Model Architecture Slection and Training
5. Model Evaluation


# 1. Data Collection
although there are readily available wikipedia hindi articles and it has 180k articles updated in 2019.so i again web scraped articles from scratch and collected 225k articles.

# 2. Data Pre-processing
it is data cleaning.removed html tags and links.converted english numericals into hindi numericals.stored it in utc-08 format.

# 3. Tokenization
Trained custom tokenizer with the help of sentencepiece python library and bpe(byte pair encoding) method.also compared this tokenizer on different dataset that contain 1047 text files.

here is the comparison table:
| Tokenizer        | vocab_size | avg_oov_rate | avg_tokens_per_word | avg_speed   | special_tokens |
|------------------|------------|--------------|---------------------|-------------|----------------|
| Custom Tokenizer | 30100      | 0            | 1.14                | 189986.44   | 6              |
| IndicBERT        | 200000     | 0            | 1.43                | 153854.09   | 7              |
| MuRIL            | 197285     | 0            | 1.17                | 190645.49   | 5              |
| XLM-R            | 250002     | 0            | 1.35                | 93933.83    | 7              |


# 4. Model selection and training

i have selected gpt2 architecture to train my model.but i have chaged its positional encoding to RoPE-ALiBi PE combination.
model configuration:
| Parameter   | Value |
|-------------|-------|
| vocab_size  | 30100 |
| n_positions | 256   |
| n_ctx       | 256   |
| n_embd      | 512   |
| n_layer     | 6     |
| n_head      | 8     |
| dropout     | 0.1   |


# 5. Model Evaluation
i compared model with standard PE and model with my custom PE with same configuration.this is comparison table for it.
| Model               | Parameters | Training Time (10 Epochs) | Perplexity |
|---------------------|------------|----------------------------|------------|
| GPT-2 (Learned PE)  | 34.4064M   | 104 hours                  | 219.20     |
| GPT-2 (RoPE + ALiBi)| 34.4576M   | 84 hours                   | 202.80     |
