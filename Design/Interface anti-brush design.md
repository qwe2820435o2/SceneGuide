# Interface anti-brush design

## Common anti-brush strategies

* Request parameters with signature for identity verification

    Can use SHA256, RSA algorithm for encryption
* Integrated man-machine verification
    
    Such as Google reCaptcha
* Request behavior control

    Including real-time behavioral analysis and offline analysis

## Practical anti-brush design

Even if the client obfuscates the code or adds the shell, as long as the attacker is patient, it is still able to crack the signature encryption algorithm

At present, the most effective preventive measure is man-machine verification

The reality is that the old version is already on the app market, and there is no way to update the code

We can only think about behavioral risk control

### H5 Interface
> The H5 page has no version problems and can be updated directly, so the man-machine verification can be used directly

**Prevention method：**
1. Integrated man-machine verification
2. Request parameters with signature for identity verification
3. 

### Client interface