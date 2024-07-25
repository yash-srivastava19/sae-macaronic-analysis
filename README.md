# sae-macaronic-analysis
Link to charts : [Dropbox](https://www.dropbox.com/scl/fo/f31smthooc966yb8ec7g5/AJuRPTfYsJPGsksDRwJLsiQ?rlkey=dy079kbj1jozrlzny0qkms59l&st=iondcnbx&dl=0)
filename_format = "{hookname}\_{max of features investigated}\_{type of prompt}\_{prompt number}\_vis.html"
- hookname: Names like `blocks.0.hook_resid_pre` or `blocks.0.hook_mlp_out`
- max of features investigated: features are mostly takes as `range(N)`, so the value is `N-1`
- type of prompt: `eng` for english prompt, `hing` for hinglish prompt.
- prompt number: there are 8 prompts, numbered 0-7

Here are the english prompts : 
1. "She loves to sing Bollywood songs" 
2. "He prefers to eat spicy Indian food." 
3. "She enjoys shopping for traditional dresses."
4. "He wants to travel to exotic locations."
5. "She enjoys reading mystery novels."
6. "They are planning a trip to the mountains."
7. "He is a fan of Bollywood movies."
8. "They are attending a wedding next month."

Here are the hinglish prompts : 
1. "She loves to sing Bollywood gaane"
2. "He prefers to eat spicy Indian khana."
3. "She enjoys shopping for traditional kapde."
4. "He wants to travel to exotic jagah."
5. "She enjoys reading mystery kahaaniyan."
6. "They are planning a trip to pahad."
7. "He is a fan of Bollywood filme."
8. "They are attending a shaadi next month."

Example a valid file name is: `blocks.2.hook_resid_pre_9_eng_2_vis.html`, which contains data for 2nd block in residual, with features `range(10)`, and the third english prompt.

## Introduction
Sparse Autoencoders have been gaining traction in the mechanistic interpretability field due to their ability to learn compact and efficient representation. SAEs apply a sparsity constraint on the hidden layer, encouraging fewer active neurons - and therefore help disentangle features(allowing each neuron to specialize in a specific set of concepts).

Macaronic languages is an expression using a mixture of languages. In this experiment, we aim to find how the model deals with inputs like these. In classic NLP, "interlingua" is a language independent representation that aims to map concepts that are common across languages. This inherently involves capturing polysemy — the ability of a word or phrase to have multiple meanings. For a language like Hinglish which has the script in English but meanings in Hindi, can we expect the model to capture semantic meaning of a given prompt? Can the model fire the same neuron, say for example "gaana"(गाना) and "song"?

My aim with this study is to try to identify whether a model has this polysemy circuit which captures the semantic meaning in this hybrid language.

**Hypothesis:** Does gpt2-small model capture the semantic meaning in a hybrid(macaronic) language like Hinglish?

## What are we going to investigate?
The main task in this study is to identify if the model fires the same neuron for both english and hinglish prompts, which only differ at one word. If the model does capture the semantic meaning of that one word, we can expect the same neurons to fire for both cases.

Without loss of generality, we can assume that capturing semantic meaning of the input prompt involves either to form complex non-linear relations(which we can extract from MLP section) or it to have deep contextual information about the language(which we can extract from Residual section). Since our task has nothing to do with token manipulation, we will not be exploring the attention section of the model.For tasks such as Indirect Object Identification, it makes sense to use the attention section, but not for our case, where we are dealing with deep contextual relations..So, the SAE we are going to investigate to find our circuits are(made available through SAE lens) : 

Residual section of gpt2-small : Provided by JBloom
MLP section of gpt2-small : Provided by Tom Mcgrath

The reason to use SAEs in this experiment is to strike a balance between sparsity and polysemanticity, and testing whether the model has learned compact and efficient representations while capturing multiple concepts(from both languages) in each neuron.
