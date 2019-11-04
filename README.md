Japanese Verb Conjugator
================
Changes the formality of the main verb in a kytea-tokenized Japanese sentence.

* [Requirements](#requirements)
* [Usage](#usage)
  * [Preprocess Data](#preprocess-data)
	* [Convert to Informal](#convert-to-informal)
	* [Convert to Polite](#convert-to-polite)
	* [Convert to Formal](#convert-to-formal)
* [Version History](#version-history)
* [Author](#author)
* [License](#license)

Requirements
------------
Requires [python 3](https://www.python.org/download/releases/3.0) and [KyTea morphological analyzer](http://www.phontron.com/kytea)

Usage
------------
```
usage: conjugator.py [-h] [-i INFILE] [-f FORMAT] [-v]

Changes the formality of the main verb in a kytea-tokenized Japanese input
sentence

optional arguments:
  -h, --help            show this help message and exit
  -i INFILE, --infile INFILE
                        Path to input file (default: stdin)
  -f FORMAT, --format FORMAT
                        Output verb conjugation format (options:
                        informal|polite|formal, default=polite)
  -v, --verbose         Enable debug logging
```

### Preprocess Data ###
```
echo "トマトを半分に切りました。" | kytea -out full
トマト/名詞/とまと を/助詞/を 半分/名詞/はんぶん に/助詞/に 切/動詞/き り/語尾/り ま/助動詞/ま し/語尾/し た/助動詞/た 。/補助記号/。
```

### Convert to Informal ###
```
echo "トマトを半分に切りました。" | kytea -out full | conjugator.py --format informal --verbose
DEBUG [2019-08-15 11:19:34,575]: Enabled debug logging
DEBUG [2019-08-15 11:19:34,575]: Converting to informal
DEBUG [2019-08-15 11:19:39,236]: Tokens: [トマト を 半分 に 切 り ま し た 。]
DEBUG [2019-08-15 11:19:39,236]: Tags: [名詞 助詞 名詞 助詞 動詞 語尾 助動詞 語尾 助動詞 補助記号]
DEBUG [2019-08-15 11:19:39,237]: Found main verb: [切 り ま し た]
DEBUG [2019-08-15 11:19:39,237]: stem = [切]
DEBUG [2019-08-15 11:19:39,237]: suffixes = [り ま し た]
DEBUG [2019-08-15 11:19:39,237]: Identified as pattern: [v5r]
DEBUG [2019-08-15 11:19:39,238]: Converted [切 り ま し た] to [切 っ た]
トマト を 半分 に 切 っ た 。
```

### Convert to Polite ###
```
echo "トマトを半分に切った。" | kytea -out full | conjugator.py --format polite --verbose
DEBUG [2019-08-15 11:18:22,518]: Enabled debug logging
DEBUG [2019-08-15 11:18:22,518]: Converting to polite
DEBUG [2019-08-15 11:18:27,158]: Tokens: [トマト を 半分 に 切 っ た 。]
DEBUG [2019-08-15 11:18:27,158]: Tags: [名詞 助詞 名詞 助詞 動詞 語尾 助動詞 補助記号]
DEBUG [2019-08-15 11:18:27,158]: Found main verb: [切 っ た]
DEBUG [2019-08-15 11:18:27,159]: stem = [切]
DEBUG [2019-08-15 11:18:27,159]: suffixes = [っ た]
DEBUG [2019-08-15 11:18:27,159]: Identified as pattern: [v5r]
DEBUG [2019-08-15 11:18:27,159]: Converted [切 っ た] to [切 り ま し た]
トマト を 半分 に 切 り ま し た 。
```

### Convert to Formal ###
```
echo "トマトを半分に切った。" | kytea -out full | conjugator.py --format formal --verbose
トマト を 半分 に お 切り し ま し た 。
```

Author
------------
Weston Feely

Citation
------------
When referencing this work, please cite this paper:

[Controlling Japanese Honorifics in English-to-Japanese Neural Machine Translation](https://www.aclweb.org/anthology/D19-5203.pdf)
```
@inproceedings{Feely:19,
  author    = {Weston Feely and Eva Hasler and Adrià de Gispert},
  title     = {Controlling Japanese Honorifics in English-to-Japanese Neural Machine Translation},
  booktitle = {Proceedings of the 6th Workshop on Asian Translation},
  year      = {2019},
  location  = {Hong Kong},
}
```

License
-----------
MIT license
https://opensource.org/licenses/MIT
