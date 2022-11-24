# lemonade public


**Endpoint:** https://rest.pollinations.ai/pollen

**Request Method:** POST

**Content-Type:** json

**Authorization**: token passed via `Authorization: Bearer [token]` header


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

Consult the file [test.html](test.html) for example usage. 

The authentication token can be set in the console with `localStorage.token = "[tokeny]"` or supplied via the form.