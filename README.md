# lemonade public


**Endpoint:** https://rest.pollinations.ai/pollen

**Request Method:** POST

**Content-Type:** json

**Authorization**: token passed via `Authorization: Bearer [token]` header


**Expected JSON structure for POST request:**
```
{
    "image": replicate:pollinations/lemonade-preset
    "input": {
        "image": [base64 encoded image],
        "styles": "archer",  // archer, modern disney, arcane work well atm.
        "num_images_per_style": 1,
        "ethnicity": "",
        "gender": ""
    }
}
```

Notes:
- The image is expected to be square with mostly the face of the person visible
- Ethnicity and gender will be inferred from the input image if not provided
- If you want to 
- After a period without use, the GPU instances the run the AI models are scaled down to zero. If you send the first request it could take a few minutes to return the first results but should then be responsive (20 seconds per request)

**API Response format:**
```
{
    "input": { [provided inputs] },
    "output": {
        "avatars": ['https://replicate.delivery/pbxt/rQVeFloN3KRNeUbz44aIPlRZCfJdHZoa2cceDOvOsySXieZAC/avatar_0.png', ...],
        "answers": {
            "hairstyle": "long", 
            "hair_color": "gray", 
            "ethnicity": "asian", 
            "hat": "none", 
            "beard": "none", 
            "moustache": "none", 
            "age": "30", 
            "skin_type": "asian", 
            "skin_color": "white", 
            "glasses": "none", 
            "gender": "female"
        },
        "prompt": [prompt created for image generation (only needed for debugging)]
    }
}
```


Consult the file [test.html](test.html) for example usage. 

The authentication token can be set in the console with `localStorage.token = "[tokeny]"` or supplied via the form.