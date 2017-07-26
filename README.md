# bibtex-js 

Library for parsing BibTeX .bib files, based mostly on the excellent guide to BibTeX, [Tame the BeaST](http://tug.ctan.org/info/bibtex/tamethebeast/ttb_en.pdf). 

Written in Typescript, compiled to ES5 Javascript (with typings provided).

This module literally just parses a BibTex file and processes it **as far as BibTeX goes**. It doesn't process TeX command (i.e., `{\"o}` is not translated to `ö`). If you want to actually work with a bibliography, look for [Bibliography.js](https://github.com/digitalheir/bibliography-js).

## Implementation
Not all internal BibTeX functions are implemented, simply because I don't need them personally. Most notably [sorting entries is still an open issue](https://github.com/digitalheir/bibtex-js/issues/1) because BibTeX has a little complicated algorithm which required a function that "purifies" field values, which for example makes `{\ss}` equivalent to `ss` but makes `ä` come after `z`. I am unsure if that is actually what anyone wants in modern days though. A modern approach would be to use Unicode collation and then sort.

[]Pull requests and issues are welcome.](https://github.com/digitalheir/bibtex-js/issues)

## Usage

```js
import {parseBibFile} from "bibtex";

const bibFile = parseBibFile(`

@InProceedings{mut2011,
  author    = {Pradeep Muthukrishnan and Dragomir Radev and Qiaozhu Mei},
  title     = {Simultaneous Similarity Learning and Feature-Weight Learning for Document Clustering},
  booktitle = {Proceedings of TextGraphs-6: Graph-based Methods for Natural Language Processing},
  month     = {June},
  year      = {2011},
  address   = {Portland, Oregon},
  publisher = {Association for Computational Linguistics},
  url       = {http://www.aclweb.org/anthology/W11-1107},
  pages = {42--50}
}
`);

console.log(
    // Keys are case-insensitive
    bibFile.getEntry("MUT2011").getField("TITLE")
); // Prints some complicated string
```

## License
MIT