### process
1. takes a list of characters.
2. tries to create chunks based on splitting on the first character
3. if any chunks are too large, then moves onto the next character

**default split characters = \["\n\n", "\n", " ", ""\]** 

### hyperparameters
- length_function : how length of chunks is calculated
- chunk_size : the maximum size of chunks
- chunk_overlap : the maximum overlap between chunks. it can be nice to have some overlap to maintain some continuity between chunks
- add_start_index : whether to include the starting position of each chunk within the original document in the metadata

