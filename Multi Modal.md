`Option 1:`
- Use multimodal embeddings (such as [CLIP](https://openai.com/research/clip)) to embed images and text
- Retrieve both using similarity search
- Pass raw images and text chunks to a multimodal LLM for answer synthesis

`Option 2:`
- Use a multimodal LLM (such as [GPT4-V](https://openai.com/research/gpt-4v-system-card), [LLaVA](https://llava.hliu.cc/), or [FUYU-8b](https://www.adept.ai/blog/fuyu-8b)) to produce text summaries from images
- Embed and retrieve text
- Pass text chunks to an LLM for answer synthesis

`Option 3:`
- Use a multimodal LLM (such as [GPT4-V](https://openai.com/research/gpt-4v-system-card), [LLaVA](https://llava.hliu.cc/), or [FUYU-8b](https://www.adept.ai/blog/fuyu-8b)) to produce text summaries from images
- Embed and retrieve image summaries with a reference to the raw image
- Pass raw images and text chunks to a multimodal LLM for answer synthesis
