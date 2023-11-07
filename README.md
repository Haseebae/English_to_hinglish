# English to Hinglish 

Assets : https://drive.google.com/drive/folders/1uIgZXHYqmdxCciT-LwrPy9mFVIRroibv?usp=sharing

- English to Hinglish translation model with relevant code switched output translation (Hindi and English)

- Criteria: 
1. Translation accuracy
2. Easily Interpretable (should resemble a casual speaker)
3. relevant "code-mixing" (English words within the translation)

### Existing methodologies:
- For translation accuracy, a pre-trained English-to-Hindi model can be inferred.
- The translation and input can then be compared and appropriately parsed to replace Hindi words with English counterparts.
- This work would primarily focus on better parsing mechanisms but it will never capture a casual tone. (Which is what I tried to address)

### Approach:
- findnitai/english-to-hinglish Dataset from hugging face contains English to Hinglish translations. These translations are said in casual tones.
- This dataset will be used to make a translation model
- The output from this model is passed to a transliteration package to convert Hinglish to Hindi(Devanagari).
- The Hindi and Hinglish are compared to identify and replace Hindi words that resemble English words.
- Examples:
- <img width="306" alt="Screenshot 2023-11-06 at 11 12 33 PM" src="https://github.com/Haseebae/English_to_hinglish_LSTM/assets/75690804/9d896989-47b5-41c7-b62e-b780d4e1ac9f">

#### MODELS USED
1. Seq2Seq LSTM
2. Seq2Seq Transformer

- First, the LSTM was trained. This model introduced numerous challenges mentioned in detail below.
- To combat this, a transformer model was used. Details below.

##### 1. Seq2Seq LSTM:

- Training Data and Example output:
- <img width="384" alt="Screenshot 2023-11-07 at 12 22 07 AM" src="https://github.com/Haseebae/English_to_hinglish_LSTM/assets/75690804/01b73998-73a8-4de7-8533-78a126ce784a">

- This Model is trained to give similar "Hinglish" outputs which are then transliterated to Devanagari Hindi
- The Devanagiri text is then parsed for direct English translations which are then replaced with the English counterparts.
##### Training Compute Challenges:
- Same output regardless of different inputs (Not trained enough)
- Too long to train

##### Seq2Seq Training Architecture:

![seq2seq Lucidchart](https://github.com/Haseebae/English_to_hinglish_LSTM/assets/75690804/4aadaed3-6b0c-4665-a98d-92575c859d0c)
- The script for training includes cells that can be used to load checkpoints and continue training
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

##### Seq2Seq Transformer:


#### Pending Work:
- Train the model for more epochs to get reasonable outputs. (Seq2Seq model performance cannot be inferred  merely from precision and loss)
- Modify the architecture to include beam search which is recommended to use with seq2seq models for increasing performance.
- Calculate BLEU Score for the actual decoded Hinglish and the ground Truth (This was not yet included as the model has to first be sufficiently trained)

#### Alternate Approach:
- Rather than making a model from scratch, Existing models can be finetuned on this dataset.
- To do this, The Hinglish TOP Dataset would need to completely be transliterated to Devanagari Hindi which is the type of data needed for finetuning existing models.
- The output from this finetuned model would be very useful and practical but would not match the required output of the assignment.
- To get the required output specified in the assignment, A hindi to english transliteration model needs to be used, Which can then be used to change it into the required format


   


