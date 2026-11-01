# Extraction record
- Model: Claude (Anthropic), claude.ai chat
- Date: 31 October 2026
- Prompt: prompt/prompt.txt (the full version sent is extraction/full_prompt.txt)
- Output as received: extraction/llm_output.json
- Verification: every phrase must occur word for word in the story and under one sub-type only.
- Researcher rejections: none
- Matching in Step 6: whole words, case-insensitive, longest phrase first, no stretch of text counted twice; stoplist: ['at present']
