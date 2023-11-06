## English to Hinglish Seq2Seq LSTM with Attention

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

##### Seq2Seq Architecture:
![seq2seq Lucidchart](https://github.com/Haseebae/English_to_hinglish_LSTM/assets/75690804/4aadaed3-6b0c-4665-a98d-92575c859d0c)


   

Assets : https://drive.google.com/drive/folders/1uIgZXHYqmdxCciT-LwrPy9mFVIRroibv?usp=sharing
