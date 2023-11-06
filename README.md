## English to Hinglish Seq2Seq LSTM with Attention

Assets : https://drive.google.com/drive/folders/1uIgZXHYqmdxCciT-LwrPy9mFVIRroibv?usp=sharing

- English to Hinglish translation model with relevant code switched output translation (Hindi and English)

- Criteria: 
1. Translation accuracy
2. Easily Interpretable (should resemble a casual speaker)
3. relevant "code-mixing" (English words within the translation)

#### Existing methodologies:
- For translation accuracy, a pre-trained English-to-Hindi model can be inferred.
- The translation and input can then be compared and appropriately parsed to replace Hindi words with English counterparts.
##### Future work here would involve fine-tuning the model and improving parsing methods to improve interpretability

#### Approach:
- This approach focuses on tackling the casual mixed Hindi tone from the ground up.
- Hinglish TOP Dataset was used to train a Seq2Seq LSTM model with Attention to train this model. (Agarwal, Anmol, et al. "CST5: Data Augmentation for Code-Switched Semantic Parsing." arXiv preprint arXiv:2211.07514 (2022).)
- Examples:
- <img width="306" alt="Screenshot 2023-11-06 at 11 12 33 PM" src="https://github.com/Haseebae/English_to_hinglish_LSTM/assets/75690804/9d896989-47b5-41c7-b62e-b780d4e1ac9f">
- This Model is trained to give similar "Hinglish" outputs which are then transliterated to Devanagari Hindi
- The Devanagiri text is then parsed for direct English translations which are then replaced with the English counterparts.

##### Seq2Seq Training Architecture:
- The script for training includes cells that can be used to load checkpoints and continue training
![seq2seq Lucidchart](https://github.com/Haseebae/English_to_hinglish_LSTM/assets/75690804/4aadaed3-6b0c-4665-a98d-92575c859d0c)

##### Inference:
###### The inference script can be run from top to bottom in one go.
- The trained model is loaded into the inference script.
- It is set up in such a way that models can be switched out with newer models.
- The seq2seq model is broken apart into the encoder and decoder.
- Working:
1. The English text is encoded and sent to the encoder
2. The encoded text is sent to the decoder to give the decoded text.
3. This text is transliterated to Devanagari Hindi.
4. The Devanagari Hindi and the decoded Hinglish text is compared to swap relevant text to give the final output.

#### Pending Work:
- Train the model for more epochs to get reasonable outputs. (Seq2Seq model performance cannot be inferred  merely from precision and loss)
- Modify the architecture to include beam search which is recommended to use with seq2seq models for increasing performance.
- Calculate BLEU Score for the actual decoded Hinglish and the ground Truth (This was not yet included as the model has to first be sufficiently trained)


   


