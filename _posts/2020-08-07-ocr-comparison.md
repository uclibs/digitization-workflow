---
layout: post
title: OCR: Who Does it Best?
date: 2020-08-07
---

As James and I settle into our new work-from-home routine, we've worked
hard on creating new digital collections workflows, policies, and
guidelines for UC Libraries.

After we finished some foundational policies, such as our new [Collection Strategy](/collection-strategy.md)
and [Digitization Selection Guidelines](/digitization-selection-guidelines.md),
we turned our attention to answering some of the more detailed workflow questions.
One big challenge we're facing is how to make our collections accessible
while working with limited staffing and resources.

We know that Optical Character Recognition (OCR) is a facet of
accessibility that has the biggest impact on whether or not our
collections are accessible, so we decided to focus our efforts on this
starting point. Our goal was to test different OCR softwares in order to
determine which was the most accurate, and decide which was the best fit
for our specific digitization workflow.

We tested a mix of five proprietary and open source softwares that we
had access to: ABBYY Finereader for Mac, Google Cloud Vision,
Tranksribus, Equidox, Adobe Acrobat Pro, and Tesseract. We then used the
Levenshtein distance[^1] to calculate the accuracy of the output from
each program:

> "Levenshtein distance (LD) is a measure of the similarity between two
> strings, which we will refer to as the source string (*s*) and the
> target string (*t*). The distance is the number of deletions,
> insertions, or substitutions required to transform *s* into *t*."

In our case, the target string was a human-generated control that either
James or I transcribed from the original document. We used a Python
library to calculate the Levenshtein distance of each output when
compared to our control, and conducted a total of six tests. We'd like
to do more tests in the future with a wider selection of documents, but
we were eager to analyze our results after the first six.

**Test One**

![Test One](https://uclibs.github.io/digitization-workflow/assets/US-80-9_b01_f02_002-test1.jpg)

This image had a total of 1542 characters.

  ABBYY   Google C.V.   Transkribus   Equidox   Acrobat Pro   Tesseract
  ------- ------------- ------------- --------- ------------- -----------
  64      30            38            135       153           45

**Test Two**

![Test Two](https://uclibs.github.io/digitization-workflow/assets/US-80-9_b01_f04_004-test2.jpg)

This image had a total of 2363 characters.

  ABBYY   Google C.V.   Transkribus   Equidox   Acrobat Pro   Tesseract
  ------- ------------- ------------- --------- ------------- -----------
  137     113           97            293       1267          138

**Test Three**

![Test Three](https://uclibs.github.io/digitization-workflow/assets/US-80-9_b04_f04_004-test3.jpg)

This image had a total of 2790 characters.

  ABBYY   Google C.V.   Transkribus   Equidox   Acrobat Pro   Tesseract
  ------- ------------- ------------- --------- ------------- -----------
  190     109           76            603       265           277

**Test Four**

![Test Four](https://uclibs.github.io/digitization-workflow/assets/US-80-9_b02_f03_003-test4.jpg)

This image had a total of 434 characters.

  ABBYY   Google C.V.   Transkribus   Equidox   Acrobat Pro   Tesseract
  ------- ------------- ------------- --------- ------------- -----------
  64      20            15            83        113           13

**Test Five**

![Test Five](https://uclibs.github.io/digitization-workflow/assets/zhdanov_1956-62_084-test5.jpg)

This image had a total of 805 characters.

  ABBYY   Google C.V.   Transkribus   Equidox   Acrobat Pro   Tesseract
  ------- ------------- ------------- --------- ------------- -----------
  58      2             10            516       175           26

**Test Six**

![Test Six](https://uclibs.github.io/digitization-workflow/assets/taftLetters_1901-10-21_1-test6.jpg)

This image had a total of 1372 characters.

  ABBYY   Google C.V.   Transkribus   Equidox   Acrobat Pro   Tesseract
  ------- ------------- ------------- --------- ------------- -----------
  1341    356           662           N/A       1343          1395

From these results, we were surprised to note that we got the best OCR
results from the open-source program Tranksribus! The caveat here is
that Tranksribus was never meant to be used as a general-purpose
typewritten OCR program. It was designed, as the name implies, to
transcribe handwritten letters, and build different Handwritten Text
Recognition (HTR) models. We just happened to get lucky finding a model
that someone else built for 19th and 20th century typewritten Dutch.
Turns out, the Dutch model did a magnificent job recognizing English as
well.

Runner up for best OCR was Google Cloud Vision. This came as no surprise
to us, as the tech giant has been making significant headway in AI
technology for some time. Honorable mentions are ABBYY Finereader for
Mac and the open-source Tesseract. Both did an admirable job on general
typewritten OCR, but fell just short of reaching the accuracy achieved
by Transkribus and Google Cloud Vision.

We got the worst results from Adobe Acrobat Pro and Equidox. These two
programs had the highest Levenshtein distances when compared to our
control text, often producing gibberish results that were impossible to
read. I would personally not use either of these programs to run OCR on
our digital collections unless absolutely necessary.

Now that we know which programs produce the most accurate OCR, we have
to weigh that against its other features, such as text editing, batch
processing, and more. Although we know that Tranksribus did the best job
on typewritten documents, it also can't efficiently handle the volume of
PDFs we create. We will, however, keep it in our toolkit for special
situations.

I hope to make a post in the near future weighing all the features of
the programs that did well on OCR: Transkribus, ABBYY Finereader for
Mac, Google Cloud Vision, and Tesseract.

[^1]: [[https://people.cs.pitt.edu/\~kirk/cs1501/Pruhs/Spring2006/assignments/editdistance/Levenshtein%20Distance.htm]{.underline}](https://people.cs.pitt.edu/~kirk/cs1501/Pruhs/Spring2006/assignments/editdistance/Levenshtein%20Distance.htm)
