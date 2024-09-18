# PDF loader and rag model implementation in preparation for Daycon's [Financial Information AI Search Algorithm Competition](https://dacon.io/competitions/official/236295/overview/description)

## dacon
This part is implementation of preprocessing before and after loading PDFs and RAG(Retrieval-Augmented Generation).  
All PDF data comes from the 'Financial Information AI Search Algorithm Competition(재정정보 AI 검색 알고리즘 경진대회)' hosted by Dacon.   
For model training code using LoRA, please refer to the following [repository](https://github.com/leeht0113/dacon_rag).  

## RAG
This directory contains modified code from the official repository of the [pymupdf4llm](https://github.com/pymupdf/RAG) library.  
Since it is based on version 0.0.10 of pymupdf4llm, we kindly ask for your understanding in uploading it independently.  
If there are any licensing issues, please contact me.  

### Modifications
pymupdf4llm contains the modified code, and pymupdf4llm_git contains the original code before modifications. The rest of the directories are the same as the original repository.  
There are the following three changes in pymupdf_rag.py file. There are comments for each modified line, marked with the phrase '!CHANGE!'.  
 * vector graphic  
   Due to the characteristics of the cluster_drawings method in fitz.Page, some insignificant small vector graphics are merged and recognized as a single image, including other areas.
   In subsequent steps, the data within this image was not properly extracted, and overlapping data issues were observed during table and text recognition.
   To address this, some conditions were added to check whether the merged image contains table or text areas.
   
 * element positioning  
   It was found that the position of the text block was not correctly recognized in cases where words were emphasized within a paragraph, causing inconsistent line spacing.
   Additionally, the tolerance for line spacing was too small, resulting in unnecessary line breaks in the text. I have modified the recognition of text block positions and line spacing.
   
 * element splitting  
   In order to organize the document by separating images and tables, the text from tables and images has been separated from the main text, and their positions are additionally provided.

## License and Copyright
All copyright-related matters follow the licenses of PyMuPDF and PyMuPDF4llm. If there are any issues, please contact me.
