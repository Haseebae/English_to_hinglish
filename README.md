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
- Examples:
- <img width="306" alt="Screenshot 2023-11-06 at 11 12 33 PM" src="https://github.com/Haseebae/English_to_hinglish_LSTM/assets/75690804/9d896989-47b5-41c7-b62e-b780d4e1ac9f">
- This dataset will be used to make a translation model
- The output from this model is passed to a transliteration package to convert Hinglish to Hindi(Devanagari).
- The Hindi and Hinglish are compared to identify and replace Hindi words that resemble English words.

- Training Data and Example output:
- <img width="384" alt="Screenshot 2023-11-07 at 12 22 07 AM" src="https://github.com/Haseebae/English_to_hinglish_LSTM/assets/75690804/01b73998-73a8-4de7-8533-78a126ce784a">

#### MODELS USED
1. Seq2Seq LSTM
2. Seq2Seq Transformer

- First, the LSTM was trained. This model introduced numerous challenges mentioned in detail below.
- To combat this, a transformer model was used. Details about this model and how to run the scripts for this are mentioned below.

### How to run the transformer model:

1. Training:
- The dataset is loaded from Hugging Face.
- The dependencies are listed in the first cell

2. Inference:
- Download the provided model from the drive link under *Seq2Seq Transformer/models*
- The model should be placed in *english_to_hinglish/Transformer/models*
- The script looks for *t_50.h5* by default. If any other model is used. change the model name in the script.
- Download the vectorization instances for English and Hinglish from the dive link under *Seq2Seq Transformer/assets/vectors*
- The vectorization instance should be placed under *english_to_hinglish/Transformer/assets/vectors*
- NOW RUN THE SCRIPT AND ENJOY

- Transformer test results :
- ![image](https://github.com/Haseebae/English_to_hinglish/assets/75690804/d96952ab-ee83-4f89-8315-e61f66271b6f)


#### MODEL DETAILS AND CHALLENGES

##### 1. Seq2Seq LSTM:

##### Challenges:
- Same output regardless of different inputs (Not trained enough even after 70 epochs)
- Too long to train
- Training time for a single epoch (20-30 mins on collab, ~10 mins on dedicated compute on GCP)
< All these challenges were addressed by migrating to the transformer architecture >

##### Seq2Seq LSTM Model Architecture:

![seq2seq Lucidchart](https://github.com/Haseebae/English_to_hinglish_LSTM/assets/75690804/4aadaed3-6b0c-4665-a98d-92575c859d0c)
- The script for training includes cells that can be used to load checkpoints and continue training
##### Inference:
###### The inference script can be run from top to bottom in one go.
- The trained model is loaded into the inference script.
- It is set up so that models can be switched out with newer models.
- The seq2seq model is broken apart into the encoder and decoder.
- Working:
1. The English text is encoded and sent to the encoder
2. The encoded text is sent to the decoder to give the decoded text.
3. This text is transliterated to Devanagari Hindi.
4. The Devanagari Hindi and the decoded Hinglish text is compared to swap relevant text to give the final output.

#### 2. Seq2Seq Transformer:

- This model was able to give reasonable and different outputs even after a single epoch
- Takes 2-5 mins to train a single epoch on Collab
- Converged very early. Due to visible overfitting, the drive link contains the model checkpoint from epoch 10, 30 and 50
- ![image](https://github.com/Haseebae/English_to_hinglish/assets/75690804/b1678650-b313-41a8-add6-7add37aa7555)


- Results from the test set:
- The test set shows accurate translations and relevant code-mixing.
< Insert image here >

##### Challenges:
- Train runtime disconnections. ( So what's new .. )
- When tested against more complicated sentences, two observations can be noted:
  1. Complex grammar throws the model off. < This can addressed with more quality data.>
  2. Some words are not being captured. < This can be addressed by increasing the size of the vocabulary during the vectorization process >

#### Seq2Seq Transformer Model Architecture:

#### Pending Work:
1. Increase vocabulary.
2. Include numbers and punctuation in the training set to improve the readability of outputs.







   


