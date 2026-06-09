# PDF support

Course: [Building with the Claude API](https://anthropic.skilljar.com/claude-with-the-anthropic-api) · Module: Features of Claude

> Lesson download: [earth.pdf](../.resources/earth.pdf)

Claude can read and analyze PDF files directly, making it a powerful tool for document processing. This works similarly to image processing, but with a few key differences in how you structure your code.

## Setting up PDF processing

To process a PDF with Claude, you'll use nearly identical code to what you'd use for images. The main differences are in the file type specifications and variable names for clarity:

```python
with open("earth.pdf", "rb") as f:
    file_bytes = base64.standard_b64encode(f.read()).decode("utf-8")

messages = []

add_user_message(
    messages,
    [
        {
            "type": "document",
            "source": {
                "type": "base64",
                "media_type": "application/pdf",
                "data": file_bytes,
            },
        },
        {"type": "text", "text": "Summarize the document in one sentence"},
    ],
)

chat(messages)
```

## Key changes from image processing

When adapting your image processing code for PDFs, update several elements:

- Change the file extension from `.png` to `.pdf`
- Update the variable name from `image_bytes` to `file_bytes` for clarity
- Set the type to `"document"` instead of `"image"`
- Change the media type to `"application/pdf"` instead of `"image/png"`

## What Claude can extract from PDFs

Claude's PDF processing capabilities go beyond simple text extraction. It can analyze and understand:

- Text content throughout the document
- Images and charts embedded in the PDF
- Tables and their data relationships
- Document structure and formatting

This makes Claude essentially a one-stop solution for extracting any type of information from PDF documents, whether you need summaries, data analysis, or specific content extraction. For example, Claude can successfully process a Wikipedia article about Earth saved as a PDF, understanding and summarizing complex document content in a single sentence.
