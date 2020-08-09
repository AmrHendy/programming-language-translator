# Programming Language Translator

This repository is build on the released Pytorch original implementation of TransCoder in [Unsupervised Translation of Programming Languages](https://arxiv.org/pdf/2006.03511.pdf) by Facebook Research in their [organization](https://github.com/facebookresearch/TransCoder).

Facebook AI Research has announced TransCoder, a system that uses unsupervised deep-learning to convert code from one programming language to another. TransCoder was trained on more than 2.8 million open source projects and outperforms existing code translation systems that use rule-based methods.

The team described the system in a paper published on arXiv. TransCoder is inspired by other neural machine translation (NMT) systems that use deep-learning to translate text from one natural language to another and is trained only on monolingual source data. To compare the performance of the model, the Facebook team collected a validation set of 852 functions and associated unit tests in each of the system's target languages: Java, Python, and C++. Compared to existing systems, TransCoder performed better on this validation set than existing commercial solutions: by up to 33 percentage points compared to j2py, a Java-to-Python translator. Although the team restricted its work to only those three languages, they claim it can "easily be extended to most programming languages."

TransCoder builds on advances in natural-language processing (NLP), in particular unsupervised NMT. The model uses a Transformer-based sequence-to-sequence architecture which consists of an attention-based encoder and decoder. Since obtaining a dataset for supervised learning would be difficult. It would require many pairs of equivalent code samples in both the source and target languages, the team opted to used monolingual datasets to do unsupervised learning, using three strategies. First, the model is trained on input sequences that have random tokens masked, the model must learn to predict the correct value for the masked tokens. Next, the model is trained on sequences that have been corrupted by randomly masking, shuffling, or removing tokens, the model must learn to output the corrected sequence. Finally, two version of these models are trained in parallel to do back-translation, one model learns to translate from the source to target language, and the other learns to translate back to the source.

![Model](https://dl.fbaipublicfiles.com/transcoder/TransCoder_Schema.jpg)
Image Source: https://arxiv.org/abs/2006.03511

To train the models, the team mined samples from over 2.8 million open-source repositories from GitHub. From that they selected files in their languages of choice (Java, C++, and Python) and extracted individual functions. They chose to work at the function level for two reasons: function definitions are small enough to be contained in a single training input batch, and translating functions allows the model to be evaluated using unit tests. Although many NLP systems use the BLEU score to evaluate their translation results, the Facebook researchers note that this metric can be a bad fit for evaluating transpilers: results that are syntactically similar may have a high BLEU score but "could lead to very different compilation and computation outputs," while programs with differing implementations that produce the same results may have a low BLEU score. Thus, the team chose to evaluate their transpiler results using a suite of unit tests. The tests were obtained from the GeeksforGeeks site by collecting problems which contained solutions written in all three target languages; this resulted in a set of 852 functions. The team compared TransCoder's performance on this test set with two other existing transpiler solutions: the j2py Java-to-Python converter and Tangible Software Solutions C++-to-Java converter. TransCoder "significantly" outperformed both, scoring 74.8% and 68.7% on C++-to-Java and Java-to-Python respectively, compared to 61% and 38.3% for commercial solutions.

In this repository, I prepared a [notebook](https://github.com/AmrHendy/programming-language-translator/blob/master/Programming_Language_Translator.ipynb) to prepare an environment and install all required dependencies to use the official TransCoder released checkpoints.

All you need now is just opening the [notebook](https://github.com/AmrHendy/programming-language-translator/blob/master/Programming_Language_Translator.ipynb) using your prefered way then run all code cells to prepare everything, then upload your source code for your chosen source language and choose the target language to which you want to translate, and wait for the MAGIC!!


## References
This Code was used to train and evaluate the TransCoder model in:

[1] M.A. Lachaux*, B. Roziere*, L. Chanussot, G. Lample [Unsupervised Translation of Programming Languages](https://arxiv.org/pdf/2006.03511.pdf).

```
@article{lachaux2020unsupervised,
  title={Unsupervised Translation of Programming Languages},
  author={Lachaux, Marie-Anne and Roziere, Baptiste and Chanussot, Lowik and Lample, Guillaume},
  journal={arXiv preprint arXiv:2006.03511},
  year={2020}
}
```

# Contribute

Contributions are always welcome!

## License

`TransCoder` is under the license detailed in the Creative Commons Attribution-NonCommercial 4.0 International license. See LICENSE for more details.
