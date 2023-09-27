split, combine, filter, manipulate documents to suit in personal applications 

### Text Splitters
want to keep the semantically related pieces of text together.
and semantically related depends on **the type of text**

text spliter works as following:
1. Split the text up into small, semantically meaningfull chunks(often sentences)
2. Start combining these small chunks into a larger chunk until you reach a certain size
3. Once you reach that size, make that chunk its own piece of text and then start creating a new chunk of text with some overlap

it means you have to decide below:
1. How the text is split
2. How the chunk size is measured

recommended text spliter -> [[RecursiveCharacterTextSplitter]] 