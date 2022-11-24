# lemonade public


**endpoint:** https://rest.pollinations.ai/pollen

**method:** POST

**expected content type:** json

**authorization**: token passed via `Authorization: Bearer [token]` header


**expected JSON structure for POST request:**
```
{
    "image": replicate:pollinations/lemonade-preset
    "input": {
        "image": [base64 encoded image],
        "styles": "styles",
        "num_images_per_style": "num_images_per_style"
    }
}
```

consult the file [test.html](test.html) for example usage