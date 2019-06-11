## Introductions
This project explores the Multi-Element Long Distance Dependency (ME-LDD) in sequential datasets and it's apparent impact on the Language Models (LMs). To synthesize ME-LDDs, we make use of Strictly _k_-Piecewise (SP-_k_) grammar. By controlling _k_ in the grammar, we are able to control the number of elements in the dependency structure.

## Prerequisite
- [Foma](https://fomafst.github.io/)
- Python 3.6

## Strictly _k_-Piecewise Datasets
SP-_k_ are _sub-regular_ grammars. SP-_k_ strings are generated using Foma tool. Our datasets contain strings of length from 60 to 100 in similar proportion.

## How to generate the datasets
1. Select value of _k_
   - Every dataset is generated for a specific value of _k_.
2. Select _Vocabulary Size_
   - In our case we select 2 vocabulary sizes: 4 and 26.
   - For vocabulary size of 4, _k_ = {2, 4, 8, 16}
   - For vocabulary size of 26, _k_ = {2, 4, 6, 8}
3. Select appropriate _Forbidden Subsequences_
   - Forbidden subsequences allow for complex grammars
   - E.g. for _k_=2, we choose {ab, bc, cd, dc}.
4. Select String Length
   - Foma generates SP-_k_ strings of a particular length. Hence, we are required to generate strings of all the lenghts one by one and then append them in a dataset.
5. Use foma to generate strings

### Generate Strings using foma
Based on the selections above, use foma commands as shown below to generate the strings
```
define Exp(A,X) ~[?* <> X] & A^90;
define G Exp([a|b|c|d],[ a b | b c | c d | d c ]);
regex G;
print random-words 100000
```
These commands produce strings of size 90; with vocabulary of {a, b, c, d}, vocabulary size of 4; and forbidden strings of {ab, bc, cd, dc}. These commands generate 100000 strings.

One can also store all these commands in a _.foma_ script file and run using
```
foma -f <filename>.foma
```
### Generate the Dataset for SP-_k_

## Language Models Trained
- [Transformer-XL](https://github.com/kimiyoung/transformer-xl)
- [AWD-LSTM](https://github.com/salesforce/awd-lstm-lm)

<!--## Please cite the paper
```
Hello
```-->
