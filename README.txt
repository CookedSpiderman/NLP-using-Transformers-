# NLP Using Transformers - Metamorphosis

## Project Description

This project applies pretrained Transformer models to Franz Kafka's *Metamorphosis* for four natural language processing tasks:

- Text summarization
- English-to-Spanish machine translation
- Extractive question answering
- Text generation

The text is loaded directly from Project Gutenberg and processed in Google Colab.

## Dataset

Book: *Metamorphosis* by Franz Kafka  
English translation: David Wyllie  
Source: Project Gutenberg eBook #5200

https://www.gutenberg.org/ebooks/5200

The plain-text version of the book is downloaded directly in the notebook using a public Project Gutenberg URL. No local dataset path is required.

## Recommended Environment

Google Colab with a T4 GPU is recommended.

To enable the GPU:

1. Open **Runtime**.
2. Choose **Change runtime type**.
3. Select **T4 GPU** as the hardware accelerator.
4. Save the setting.

## Required Libraries

The notebook uses:

- PyTorch
- Hugging Face Transformers
- sentencepiece
- requests
- NumPy
- Matplotlib
- evaluate
- rouge_score
- sacrebleu

Required packages are installed inside the notebook where necessary.

## Running the Notebook

1. Open the submitted notebook in Google Colab.
2. Enable a T4 GPU.
3. Run the cells from top to bottom.
4. The book is automatically downloaded from Project Gutenberg.
5. The Gutenberg header and footer are removed and the text is cleaned.
6. The book is tokenized and divided into smaller chunks where necessary.
7. Run the summarization section to generate and evaluate summaries with DistilBART.
8. Run the machine translation section to translate a passage from English to Spanish using MarianMT.
9. Run the question-answering section to ask questions about a selected passage using DistilBERT.
10. Run the text-generation section to generate continuations with SmolLM2 using different temperature settings.

The first execution of each section may take longer because pretrained model weights must be downloaded from Hugging Face.

## Models Used

### Summarization
Model: `sshleifer/distilbart-cnn-12-6`

Three decoding configurations were compared by changing beam search and output length. ROUGE scores and qualitative analysis were used for evaluation.

### Machine Translation
Model: `Helsinki-NLP/opus-mt-en-es`

English passages from *Metamorphosis* were translated into Spanish. Greedy decoding and four-beam search were compared using BLEU.

### Question Answering
Model: `distilbert/distilbert-base-cased-distilled-squad`

The model performs extractive question answering by identifying the most likely answer span inside a passage from the book. An interactive chatbot function is included in the notebook.

### Text Generation
Model: `HuggingFaceTB/SmolLM2-360M-Instruct`

Text generation was performed from a seed passage taken from the beginning of *Metamorphosis*. Temperatures of 0.2, 0.7, and 1.5 were compared while top-p was kept at 0.9. Perplexity and qualitative analysis were used to compare the outputs.

## Assumptions

The pretrained models were used for inference rather than being trained from scratch. Because Transformer models have sequence-length limitations, the full book could not always be processed as one input and was divided into smaller token-based sections when necessary.

The question-answering model is extractive and therefore requires the relevant book passage to be supplied as context. It is not designed to search the entire novella automatically.

ROUGE and BLEU depend on overlap with reference text, so quantitative scores were interpreted together with qualitative inspection of the generated outputs.

## Submission Files

- Transformer project `.ipynb` notebook with saved outputs
- Project report in PDF format
- `README.md`

The Project Gutenberg text file does not need to be included because the notebook downloads it directly from its public URL.