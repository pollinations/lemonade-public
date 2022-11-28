# Lemonade API


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
        "strength": 0.6, // how much to change the image
        "ethnicity": "",
        "gender": ""
    }
}
```

Notes:
- The image is expected to be square with mostly the face of the person visible
- Ethnicity and gender will be inferred from the input image if not provided
- After a period without use, the AI model instances are scaled down to zero. If you send the first request it could take a few minutes to return the first results but should then be responsive (20 seconds per request)

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

## Websocket Endpoint

```
import WebSocket from 'ws';

const ws = new WebSocket(endpoint_url);

ws.on('open', function open() {
    console.log('connected');

    const request = {
        "image":"replicate:pollinations/lemonade-preset",
        "input": {
            "image":"data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAIAAACQkWg2AAADIElEQVR4nAAQA+/8Ame7A9yY2g+Vat11/fVkl/NS7O+k9bd6KYtDMjzG5q4OnBOoZ1cyhuLEuHEABjpwqAN58wwf5APC2lNtD301Jj0qCFuIdcgNroK9MqajHOikCmCEeL+ggZbzJfXAJ0O2IdME7OMTRo5dCSzzEXlGssNdE1SKDUQGw9rFzK8IuOFo+KoxYkSM2hMoVpW04+QYDaFqARgsty0fuhnxDM/ZHbDf2i4lKn05n8WgsIXFM8r5lQgmpwojLLdIIBE+ye2yro64AgE/yvxdQKQmUDJwJ7xu4UI8WjtK+a6Xtgtr+hiW/Fc1IsRHdB6qJioHmg/703HZFBAA49Eh3Twxw57s9bPz0zypGT8MJv4vwS/fwIO3zLkT7z82a4t2DLzB4JGtPLsqtMxkABXYhXtOBzYWVSeCZB3WYAWMtprZC/PvHK3695gT9bpfXxXbVep2Fd5Pq/XpPGLIQwPdzeTlNeQpIdX9G8n2clX3fYtfGkIKrJDXSZzkvgNWA3ml4EPrbGM74dWZpp294/AAz2+ovG4GH4vux27yqOaoXlYq7Q23zAjF3aSVAuIMBqPB5GZgKWA4z7AwDM8GvlMUAw/1HXM8d3GK2BFBJF15+ub9xIRBVxDgBAkEGjviL5srqPIOSC/0jgcl3bBr03+t9QSr0jgd9boULC2zqbiQZK3iD2rVS5g9qeiYJHNLxMfu/HyM2FpOYQPpSQQKpxXMgNwDcd3rYD8pXLaN7JEvNOnjqTqgMs4tCn4R/1tzQqqjdb2fjynR8QgYMFMTI9vhfxBxAP67w2Qv6vbp8PiD5U2thVpzJoqhEiBKD5nM8r9AF1A2Emnz6KMF9cTyYquW2MwMyQG37bJXmvEm76J9ugKPZ22uOf7s8txD3v3KyrKR+FhBxtVYI7VpE5Xy3cD6epykeJgBD6QD1qRjCzbYyX+O7GU9z4r/A1KzzEPF7/lAeRVNuDDY9BxYLtb7PyPy1qDmJBTOAqbNcU6FXe557yzH+vJUa8TeDxITr3cj3Swfzt2BfQcNPd5VJbUdXgRwb/cwQkVxTgEAAP//AimEcorlYhUAAAAASUVORK5CYII=",
            "styles":"archer",
            "gender":"",
            "ethnicity":""
        }
    }
    ws.send(JSON.stringify(request))

})

ws.on('message', function incoming(data) {

    // convert data from buffer to string
    const str = new TextDecoder("utf-8").decode(data);
    const json = JSON.parse(str);
    const {output, status } = json;
    console.log(output, status);
})

```


## Sample Code

Consult the file [test.html](test.html) for example usage. 

Run directly in the browser: [https://htmlpreview.github.io/?https://github.com/pollinations/lemonade-public/blob/main/test.html](https://htmlpreview.github.io/?https://github.com/pollinations/lemonade-public/blob/main/test.html)

The authentication token can be set in the console with `localStorage.token = "[tokeny]"` or supplied via the form.